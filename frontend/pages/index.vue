<template>
    <div>
        <h1>Camera Streaming</h1>
        <video ref="videoRef" width="640" height="480" autoplay></video>
    </div>
</template>

<script>
export default {
    name: 'CameraStreaming',
    mounted() {
        this.setupCamera();
    },
    methods: {
        setupCamera() {
            const video = this.$refs.videoRef;
            if(navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
                    video.srcObject = stream;
                    video.play();
                }).catch(error => {
                    console.error("カメラにアクセスできませんでした:", error);
                });
            } else {
                console.warn("お使いのブラウザにサポートされていません。");
            }
        }
    }
}
</script>
