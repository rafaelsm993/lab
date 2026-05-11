<script lang="ts">
  const src = "https://svelte.dev/tutorial/image.gif";
  let string = "<strong>This is a string in bold</strong>";
  let name = "W O R L D";
  let mainColor = "red";

  // Using the $state rune to create reactive variables
  let count = $state(0);
  let array = $state([1, 2, 3]);

  // Using the $derived rune to create a reactive variable based on other runes
  let total = $derived(array.reduce((a, b) => a + b, 0));
  
  function increment() {
    count += 1;
  }
  function addToArray(){
    array = [...array, array.length + 1];
    // DEBUGGING: Using the $inspect rune to log the current state of the array
    console.log($state.snapshot(array));
  }
  // DEBUGGING: Using the $inspect rune to log the current state of the array, $inspect 
  //  should be declared in component setup scope so Svelte can wire it once.
  $inspect(array);

  // DEBUGGING: Using the $inspect rune with console.trace to log the current state of the array along with a stack trace
  $inspect(array).with(console.trace);
</script>

<main style:--main-color={mainColor}>
  <h1>Hello {name.toLowerCase()}!</h1>
  <img {src} alt="Alternative Text" />
  <p>This is a paragraph.</p>
  <!-- Adding the @html directive so it doesn't perform sanitization -->
  <p>{@html string}</p>
  <button onclick={increment}>
    Clicked {count}
    {count == 1 ? "time" : "times"}
  </button>
  <p>Array: {array} ...</p>
  <button onclick={addToArray}>
    Add number to array
  </button>
  <p>Array sum: {total}</p>
</main>

<style lang="scss">
  p {
    color: var(--main-color);
    font-family: "Comic Sans MS", cursive;
    font-size: 2em;
  }
  button {
    background-color: var(--main-color);
    border: 2px solin var(--main-color);
    font-size: 1.5em;
    padding: 0.5em 1em;
    cursor: pointer;
  }
</style>
