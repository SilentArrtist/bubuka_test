

<template>
    <a :href="link" :class="classname" @click="startTimer">
        <div v-if="timerState && timerEnabled" class="timer">
            Отправить повторно
            <span class="timer_block">
                {{ timerValue }}
            </span>
        </div>
        <slot v-else></slot>
    </a>
</template>
<script>
export default {
    props: ['classname', 'timerEnabled', 'link'],
    data() {
        return {
            timerCount: 10,
            timerState: false,
            timerValue: null,
        }
    },
    methods: {
        startTimer() {
            if (this.timerState) return;
            this.timerValue = this.toMMSS(this.timerCount);
            this.timerState = true;
            let timer = setInterval(() => {
                if (this.timerCount == 0) {
                    clearInterval(timer)
                    this.timerCount = 10;
                    this.timerState = false;
                    return;
                }
                this.timerCount--
                this.timerValue = this.toMMSS(this.timerCount);
            }, 1000)
        },
        toMMSS(time) {
            let sec_num = parseInt(time, 10); // don't forget the second param
            let hours = Math.floor(sec_num / 3600);
            let minutes = Math.floor((sec_num - (hours * 3600)) / 60);
            let seconds = sec_num - (hours * 3600) - (minutes * 60);
            if (minutes < 10) { minutes = "0" + minutes; }
            if (seconds < 10) { seconds = "0" + seconds; }
            return minutes + ':' + seconds;
        }
    }
}
</script>

<style>
.text_btn {
    text-decoration: none;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 20px;
    line-height: 24px;
    width: fit-content;
    /* Color */
    color: #FF6E00;
    background-image: linear-gradient(90deg, #D7650F 0%, #E1250A 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    background-size: 300% 100%;
    background-position: top left;
    transition: all 0.2s ease-in-out;
}

.text_btn:hover {
    background-position: top left 100%;
}

.text_btn:active {
    background-image: linear-gradient(90deg, #853900 0%, #AA1500 100%);
    background-position: top left 100%;
}

.btn {
    text-decoration: none;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 16px 24px;
    gap: 8px;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 20px;
    display: flex;
    color: #FAFAFA;
    transition: 0.2s ease;
    background: linear-gradient(90deg, #D7650F 0%, #E1250A 100%);
    border-radius: 10px;
    transition: 0.2s ease all;
}

.btn:hover {
    background: linear-gradient(90deg, #D7650F 0%, #E1250A 100%);
    box-shadow: 0px 8px 24px rgba(215, 101, 15, 0.7);
    border-radius: 40px;
}

.btn:active {
    background: linear-gradient(90deg, #853900 0%, #AA1500 100%);
    box-shadow: none;
    border-radius: 40px;
}


.icon_btn {
    padding: 16px;
    gap: 8px;
}

.btn.disabled {
    color: #FAFAFA;
    background: linear-gradient(90deg, #8A8A8A 0%, #505050 100%);
    pointer-events: none;
}

.btn.disabled span,
.btn.disabled svg {
    opacity: 0.5;
}

.timer {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: row;
    gap: 5px;
    width: fit-content;
}

.timer_block {
    padding: 4px;
    gap: 10px;
    background: #C4250E;
    border-radius: 5px;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400;
    font-size: 13px;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: #FAFAFA;
    width: fit-content;
}
</style>
