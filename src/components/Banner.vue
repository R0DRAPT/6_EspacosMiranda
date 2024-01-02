<template>
    <div>
        <div id="Banners" :style="{ 'backgroundImage': 'url(' + currentBannerUrl + ')' }" @transitionend="transitionEnd">
            <div class="progress-bar" :style="{ width: progressBarWidth }"></div>
            <div class="arrow left" @click="changeBanner(-1)">‹</div>
            <div class="arrow right" @click="changeBanner(1)">›</div>
        </div>
    </div>
</template>

<script>
import Banner1 from '/public/img/Banner1.jpg';
import Banner2 from '/public/img/Banner2.jpg';
import Banner3 from '/public/img/Banner3.jpg';

export default {
    name: "Banner",
    data() {
        return {
            currentBanner: 1,
            totalBanners: 3,
            bannerImages: [Banner1, Banner2, Banner3],
            currentBannerUrl: Banner1,
            transitionInProgress: false,
            timerId: null, // Adiciona um identificador para o temporizador
            progressBarWidth: '0%' // Inicia a barra de progresso com largura zero
        };
    },
    methods: {
        changeBanner(direction) {
            if (this.transitionInProgress) {
                return; // Evita iniciar uma transição se outra estiver em andamento
            }

            this.transitionInProgress = true;

            // Limpa o temporizador existente
            clearInterval(this.timerId);

            // Atualiza o índice do banner com base na direção
            this.currentBanner += direction;

            // Garante que o índice do banner está dentro dos limites
            if (this.currentBanner > this.totalBanners) {
                this.currentBanner = 1;
            } else if (this.currentBanner < 1) {
                this.currentBanner = this.totalBanners;
            }

            // Atualiza a URL da imagem com base no novo índice
            this.currentBannerUrl = this.bannerImages[this.currentBanner - 1];

            // Inicia o temporizador para a barra de progresso com um atraso de 3000ms (3 segundos)
            setTimeout(() => {
                let progress = 0;
                this.progressBarWidth = '0%';

                this.timerId = setInterval(() => {
                    // Configura a largura da barra de progresso apenas no início
                    if (progress === 0) {
                        this.progressBarWidth = '0%';
                    }

                    progress += 1;
                    this.progressBarWidth = progress + '%';

                    if (progress >= 115) {
                        clearInterval(this.timerId);
                        this.transitionInProgress = false;
                        this.changeBanner(1); // Próximo banner
                    }
                }, 100);
            }, 3000); // Atraso de 3000ms (3 segundos) antes de iniciar a barra de progresso
        },
        transitionEnd() {
            // Chamado quando a transição de imagem é concluída
            this.transitionInProgress = false;
            this.progressBarWidth = '0%'; // Reinicia a barra de progresso
        }
    },
    mounted() {
        // Chama changeBanner com direção 0 para carregar o Banner1 ao iniciar
        this.changeBanner(0);
    }
};
</script>

<style scoped>
#Banners {
    position: relative;
    background-size: cover;
    height: 680px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    transition: background-image 1s ease;
    overflow: hidden; 
    position: relative;
}

.progress-bar {
    position: absolute;
    top: 0;
    left: 0;
    height: 6px;
    background-color: #9995959f; 
    transition: width 1s ease;
}

.arrow {
    position: absolute;
    top: 50%;
    font-size: 24px;
    cursor: pointer;
    color: white;
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.5);
    transition: background-color 0.3s ease;
    opacity: 0;
    transition: opacity 0.5s ease;
}

#Banners:hover .arrow {
    opacity: 1;
}

.arrow:hover {
    background-color: rgba(0, 0, 0, 0.8);
}

.left {
    left: 10px;
}

.right {
    right: 10px;
}

.arrow:hover {
    background-color: rgba(0, 0, 0, 0.8);
}
</style>