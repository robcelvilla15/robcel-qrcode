<template>
<div id="reader" style="width: px"></div>
</template>

<script>
export default {
mounted() {
const html5QrCode = new this.$html5Qrcode("reader");

html5QrCode.start(
{ facingMode: "environment" }, // back camera
{
fps: 10,
qrbox: 270
},
(decodedText, decodedResult) => {
console.log("QR Code detected:", decodedText);
},
(errorMessage) => {
// console.log("QR Code scan error:", errorMessage);
}
).catch((err) => {
console.error("Unable to start scanning.", err);
});
}
};
</script>