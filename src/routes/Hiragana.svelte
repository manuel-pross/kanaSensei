<script>
  import KanaList from "../components/KanaList.svelte";
  import Footer from "../components/Footer.svelte";

  let hiragana = [];

  fetch("./hiragana.json")
    .then((res) => {
      if (!res.ok) {
        throw new Error("Fetching meetups failed, please try again.");
      }
      return res.json();
    })
    .then((data) => {
      hiragana = data;
    });
</script>

<KanaList kana={hiragana} />
<Footer />
