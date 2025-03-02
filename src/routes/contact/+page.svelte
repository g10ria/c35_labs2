<svelte:head>
  <title>Contact</title>
</svelte:head>

<form method="GET" action="mailto:gloriazh@mit.edu" enctype="text/plain">
    <label for="uremail">Enter your email: </label>
    <input name="uremail" type="email" required />
    <label for="subject">Enter your subject: </label>
    <input type="text" name="subject" required />
    <label for="body">Enter your body: </label>
    <textarea name="body"></textarea>
    <button>submit</button>
  </form>