<script>
  let messages = [];
  let input = '';

  const sendMessage = () => {
    if (input.trim()) {
      messages = [...messages, { text: input, user: true }];
      input = '';
      
      setTimeout(() => {
        messages = [...messages, { text: "Hello!, how may i help u today ?", user: false }];
      }, 1000);
    }
  };
</script>

<style>
  .chat-container {
    display: flex;
    flex-direction: column;
    height: 80vh;
    max-width: 600px;
    margin: auto;
    border: 1px solid #ccc;
    border-radius: 8px;
    overflow: hidden;
    font-family: Arial, sans-serif;
  }

  .header {
    padding: 1rem;
    background-color: #f1f1f1;
    border-bottom: 1px solid #ccc;
  }

  .header h2 {
    margin: 0;
  }

  .header p {
    margin: 0.5rem 0;
    color: #666;
  }

  .header ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  .header ul li {
    margin: 0.5rem 0;
    color: #007bff;
    cursor: pointer;
  }

  .messages {
    flex: 1;
    padding: 1rem;
    overflow-y: auto;
    background-color: #fff;
  }

  .message {
    padding: 0.5rem;
    border-radius: 8px;
    margin: 0.5rem 0;
    max-width: 80%;
    word-wrap: break-word;
  }

  .user {
    background-color: #dcf8c6;
    align-self: flex-end;
  }

  .bot {
    background-color: #f1f1f1;
    align-self: flex-start;
  }

  .input-container {
    display: flex;
    gap: 0.5rem;
    padding: 1rem;
    background-color: #f9f9f9;
    border-top: 1px solid #ccc;
  }

  input {
    flex: 1;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 1rem;
  }

  button {
    padding: 0.5rem 1rem;
    border: none;
    background-color: #007bff;
    color: white;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1rem;
  }
</style>

<div class="chat-container">
  <div class="header">
    <h2>Welcome to SvelteKit AI Chatbot!</h2><br>

    <ul>
      <li>Explain technical concepts</li>
      <li>Summarize an article</li>
      <li>Draft an email</li>
    </ul>
  </div>
  <div class="messages">
    {#each messages as { text, user }}
      <div class="message {user ? 'user' : 'bot'}">{text}</div>
    {/each}
  </div>
  <div class="input-container">
    <input type="text" bind:value={input} on:keypress={(e) => e.key === 'Enter' && sendMessage()} placeholder="Send a message..." />
    <button on:click={sendMessage}>Send</button>
  </div>
</div>