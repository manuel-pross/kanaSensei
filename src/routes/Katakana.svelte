<script>
  import KanaList from "../components/KanaList.svelte";
  import Footer from "../components/Footer.svelte";

  let katakana = [];

  fetch("./katakana.json")
    .then((res) => {
      if (!res.ok) {
        throw new Error("Fetching meetups failed, please try again.");
      }
      return res.json();
    })
    .then((data) => {
      katakana = data;
    });
</script>

<KanaList kana={katakana} />
<Footer />
