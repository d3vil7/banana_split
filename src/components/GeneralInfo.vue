<template>
    <div class="fold">
        <h1>Banana split</h1>
        <input id="fold-header" type="checkbox" name="fold" v-model="unfolded">
        <label for="fold-header">
            <h2 v-if="unfolded">Shamir Secret Sharing for people with friends</h2>
            <p v-else>What is this?</p>
        </label>
        <div class="fold-content">
            <p>Banana Split uses <a href="https://en.wikipedia.org/wiki/Shamir%27s_Secret_Sharing">Shamir's secret sharing</a> to make your paper backups more resilient and secure.</p>
            <p>After you type in your secret into Banana Split, it will be encrypted with a autogenerated passphrase and split into N QR-codes, ready to be printed out. You'll need N/2+1 of those printouts to reconstruct the secret, and then the passphrase to decrypt it.</p>
            <p>Banana Split tries to protect your secret from the attack vectors like "attacker is able to intercept everything you're sending to your printer", and that's why you'll have to write down the passphrase on your printouts by hand.</p>
            <p>Banana Split is a self-contained HTML page, and should only be opened from your local Documents folder, while browser is in the Offline mode — this way the risk of compromise will be minimal.</p>
            <p>Recovery can be done on any device with a webcam — just show your QR codes to the webcam and follow the notifications on screen in the process.</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'GeneralInfo',
    data: function () {
        return { unfolded: true }
    },
    created: function() {
        var self = this;
        this.$eventHub.$on("foldGeneralInfo", function() {
            self.unfolded = false
        })
    }
}
</script>

<style>
.fold {
  position: relative;
  overflow: hidden;
}
.fold input {
  position: absolute;
  opacity: 0;
  z-index: -1;
}
.fold label {
  position: relative;
  cursor: pointer;
}
.fold label * {
    display: inline-block;
}
.fold-content {
  max-height: 0;
  overflow: hidden;
  -webkit-transition: max-height .35s;
  -o-transition: max-height .35s;
  transition: max-height .35s;
}
.fold input:checked ~ .fold-content {
  max-height: 100vh;
}
.fold label::before {
  display: inline;
  -webkit-transition: all .35s;
  -o-transition: all .35s;
  transition: all .35s;
}
.fold input[type=checkbox]:not(:checked) + label::before {
  content: "▶";
}
.fold input[type=checkbox]:checked + label::before {
  content: "▼";
}
</style>
