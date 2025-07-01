<script>
  import { onMount } from "svelte";

  let searchQuery = "";
  let messageInput = "";
  let activeChatIndex = 0;

  let messages = [
    {
      id: 1,
      type: "assistant",
      title:
        "ISO Certified Companies Cutting Tools Materials Made of Steel Near Me",
      content:
        "10 companies were found with ISO certification for cutting tools materials made of steel in Texas. The closest to the location you specified is company A and the furthest is company B. Companies C, D and E also manufacture equipment out of fiberglass.",
      showSources: true,
    },
    {
      id: 2,
      type: "user",
      content:
        "ISO Certified Companies Cutting Tools Materials Made of Steel Near Me",
    },
  ];

  let chatHistory = [
    "ISO Certified Companies",
    "ISO Certified Companies",
    "ISO Certified Companies",
    "ISO Certified Companies",
    "ISO Certified Companies",
    "ISO Certified Companies",
  ];

  // Add function to handle chat selection
  function selectChat(index) {
    activeChatIndex = index;
    // Here you can add logic to load different messages for different chats
    console.log(`Selected chat ${index}: ${chatHistory[index]}`);
  }
</script>

<!-- <div class="app-header"></div> -->
<div class="app-container">
  <!-- Left Sidebar -->
  <aside class="sidebar">
    <!-- New Chat Button -->
    <div class="topside">
      <button class="new-chat-btn">
        <img src="/Pansophy Button.svg" alt="add" />
        New Chat
      </button>

      <!-- Search Bar -->
      <div class="search-container">
        <input
          type="text"
          placeholder="Search the chats"
          bind:value={searchQuery}
          class="search-input"
        />
        <button class="search-btn" aria-label="Search">
          <img src="/Search.svg" alt="search" />
        </button>
      </div>
    </div>

    <!-- Chat History Header -->
    <div class="chat-history-header">
      <span>Last Chats</span>
    </div>

    <!-- Chat History List -->
    <div class="chat-history">
      {#each chatHistory as chat, index}
        <div
          class="chat-item"
          class:active={index === activeChatIndex}
          on:click={() => selectChat(index)}
          role="button"
          tabindex="0"
          on:keydown={(e) => {
            if (e.key === "Enter" || e.key === " ") {
              e.preventDefault();
              selectChat(index);
            }
          }}
        >
          <span class="chat-title">{chat}</span>
          <button
            class="more-btn"
            aria-label="More options"
            on:click|stopPropagation={() =>
              console.log("More options for chat", index)}
          >
            <img src="/Vector.svg" alt="" />
          </button>
        </div>
      {/each}
    </div>
  </aside>

  <!-- Main Chat Area -->
  <main class="main-content">
    <!-- Chat Messages -->
    <div class="messages-container">
      {#each messages as message}
        {#if message.type === "assistant"}
          <div class="message assistant-message">
            <div class="message-content">
              <h3 class="message-title">{message.title}</h3>
              <p class="message-text">{message.content}</p>

              <!-- Action Buttons -->
              <div class="message-actions">
                <button class="action-btn" aria-label="Copy message">
                  <img src="/Copy.svg" alt="copy" />
                </button>
                <button class="action-btn" aria-label="Like message">
                  <img src="/Like.svg" alt="like" />
                </button>
                <button class="action-btn" aria-label="Dislike message">
                  <img src="/Dislike.svg" alt="dislike" />
                </button>
              </div>

              {#if message.showSources}
                <button class="sources-btn">Sources</button>
              {/if}
            </div>
          </div>
        {:else}
          <div class="message user-message">
            <div class="user-message-content">
              {message.content}
            </div>
          </div>
        {/if}
      {/each}
    </div>

    <!-- Message Input -->
    <div class="input-container">
      <div class="input-wrapper">
        <textarea
          placeholder="Ask me anything"
          bind:value={messageInput}
          class="message-input"
          rows="1"
        ></textarea>

        <div class="input-actions">
          <div class="input-actions-left">
            <button class="input-action-btn" aria-label="Add attachment">
              <img src="/Plus.svg" alt="" />
            </button>
            <div class="input-actions-center">
              <button class="mode-btn">Deep Thinking</button>
              <button class="mode-btn">Search the web</button>
            </div>
          </div>

          <div class="input-actions-right">
            <button class="avatar-btn" aria-label="Send message">
              <div class="avatar">
                <img src="/Logo.svg" alt="" />
              </div>
            </button>
          </div>
        </div>
      </div>
    </div>
  </main>
</div>

<style>
  /* Global Styles */
  :global(*) {
    scrollbar-width: none;
    -ms-overflow-style: none;
    margin: 0;
    padding: 0;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    overflow: hidden;
    background: transparent;
  }

  :global(*::-webkit-scrollbar) {
    display: none;
  }

  /* Main Container */
  .app-container {
    position: fixed;
    top: 15px;
    left: 15px;
    right: 15px;
    bottom: 15px;
    width: calc(100vw - 30px);
    height: calc(100vh - 30px);
    display: flex;
    border-radius: 16px;
    background: linear-gradient(
      112.58deg,
      rgba(40, 40, 40, 0.6) 0%,  
      rgba(60, 60, 60, 0.4) 100% 
    );
    backdrop-filter: blur(40px) saturate(1.3); 
    border: 1px solid rgba(255, 255, 255, 0.18);
    box-shadow: 
      0 0 0 1px rgba(255, 255, 255, 0.08),
      0 20px 60px rgba(0, 0, 0, 0.3),
      0 8px 25px rgba(0, 0, 0, 0.15),
      inset 0 1px 0 rgba(255, 255, 255, 0.12);
    font-family: Poppins, sans-serif;
    overflow: hidden;
    box-sizing: border-box;
    z-index: 1;
  }

  /* Sidebar Styles */
  .sidebar {
    display: flex;
    flex-direction: column;
    width: 240px;
    height: auto;
    padding: 30px 16px;
    background: rgba(0, 0, 0, 0.19); 
    border-top-left-radius: 16px;
    border-bottom-left-radius: 16px;
    border-right: 1px solid rgba(255, 255, 255, 0.12);
    gap: 8px;
  }

  .topside {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 16px;
    padding-bottom: 16px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  }

  /* Assistant Message  */
  .assistant-message {
    align-self: flex-start;
    background: rgba(0, 0, 0, 0.4); 
    backdrop-filter: blur(10px); 
    border: 1px solid rgba(255, 255, 255, 0.15);
    border-radius: 16px;
    box-sizing: border-box;
    border-bottom-width: 1px;
    padding: 12px;
  }

  .new-chat-btn {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    height: 40px;
    padding: 0 12px;
    gap: 10px;
    background: rgba(0, 0, 0, 0.4);
    border: 1px solid rgba(255, 255, 255, 0.15);
    border-radius: 10px;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 500;
    line-height: 16px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .new-chat-btn:hover {
    background: rgba(0, 0, 0, 0.5);
    border-color: rgba(255, 255, 255, 0.25);
    color: white;
  }

  .search-container {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    height: 40px;
    padding: 0 12px;
    background: rgba(0, 0, 0, 0.4);
    border: 1px solid rgba(255, 255, 255, 0.15);
    border-radius: 10px;
    transition: all 0.2s ease;
    box-sizing: border-box;
  }

  .search-container:hover,
  .search-container:focus-within {
    background: rgba(0, 0, 0, 0.5); 
    border-color: rgba(255, 255, 255, 0.25);
  }

  .search-input {
    width: 100%;
    height: 16px;
    padding-right: 26px;
    background: none;
    border: none;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 400;
    line-height: 16px;
    letter-spacing: -0.01em;
    outline: none;
  }

  .search-input::placeholder {
    color: rgba(255, 255, 255, 0.5);
  }

  .search-btn {
    position: absolute;
    right: 12px;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    color: rgb(255, 255, 255);
    cursor: pointer;
    padding: 0;
    width: 14px;
    height: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s ease;
  }

  .search-btn:hover {
    color: rgba(255, 255, 255, 0.9);
  }

  .chat-history-header {
    margin-top: 6px;
    margin-bottom: 10px;
    color: rgba(255, 255, 255, 0.5);
    font-family: Poppins, sans-serif;
    font-size: 10px;
    font-weight: 500;
    line-height: 14px;
    text-transform: uppercase;
    letter-spacing: 0.4px;
  }

  .chat-history {
    display: flex;
    flex-direction: column;
    flex: 1;
    gap: 3px;
    overflow-y: auto;
  }

  .chat-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 36px;
    padding: 2px 12px;
    gap: 10px;
    background: transparent;
    border-radius: 10px;
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 400;
    line-height: 16px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .chat-item:hover {
    background: rgba(0, 0, 0, 0.2); 
  }

  .chat-item.active {
    background: rgba(0, 0, 0, 0.4); 
    border: 1px solid rgba(255, 255, 255, 0.18);
  }

  .chat-title {
    flex: 1;
    color: rgba(255, 255, 255, 0.8);
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .chat-item:hover .more-btn,
  .chat-item.active .more-btn {
    opacity: 1;
    visibility: visible;
  }

  .more-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 24px;
    height: 24px;
    padding: 4px;
    background: none;
    border: none;
    border-radius: 6px;
    color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.2s ease;
    opacity: 0;
    visibility: hidden;
  }

  .more-btn:hover {
    background: rgba(255, 255, 255, 0.1);
    color: rgba(255, 255, 255, 0.8);
  }

  /* Main Content */
  .main-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 16px 56px;
    height: 100%;
    width: 100%;
    gap: 26px;
    overflow: hidden;
    box-sizing: border-box;
    border-top-right-radius: 16px;
    border-bottom-right-radius: 16px;
  }

 .messages-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: flex-end; 
    align-items: center;
    gap: 20px;
    overflow-y: auto;
    overflow-x: hidden;
    min-height: 0;
    box-sizing: border-box;
    max-width: 800px;
    margin: 0 auto;
    width: 100%;
    padding-bottom: 10px; 
  }

  .message {
    width: 100%;
  }

  .user-message {
    align-self: flex-end;
    max-width: 300px;
    width: fit-content;
    gap: 20px;
    border-radius: 16px;
    padding: 12px;
    background: rgba(37, 99, 235, 0.6);
  }

  .message-content {
    padding: 20px;
  }

  .message-title {
    margin: 0 0 12px 0;
    color: rgba(255, 255, 255, 0.95);
    font-family: Poppins, sans-serif;
    font-size: 16px;
    font-weight: 600;
    line-height: 22px;
    letter-spacing: -0.02em;
  }

  .message-text {
    margin: 0 0 16px 0;
    color: rgba(255, 255, 255, 0.8);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 400;
    line-height: 18px;
    letter-spacing: -0.01em;
  }

  .message-actions {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 16px;
  }

  .action-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 28px;
    height: 28px;
    padding: 6px;
    background: none;
    border: none;
    border-radius: 6px;
    color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .action-btn:hover {
    background: rgba(255, 255, 255, 0.05);
    color: rgba(255, 255, 255, 0.8);
  }

  .sources-btn {
    height: 30px;
    padding: 0 14px;
    background: rgba(255, 255, 255, 0.15); 
    backdrop-filter: blur(8px); 
    border: 1px solid rgba(255, 255, 255, 0.22);
    border-radius: 15px;
    color: rgba(255, 255, 255, 0.95);
    font-family: Poppins, sans-serif;
    font-size: 10px;
    font-weight: 500;
    line-height: 14px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .sources-btn:hover {
    background: rgba(255, 255, 255, 0.22);
    border-color: rgba(255, 255, 255, 0.35);
  }

  .user-message-content {
    color: rgba(255, 255, 255, 0.95);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 400;
    line-height: 16px;
    letter-spacing: -0.01em;
    overflow-wrap: break-word;
  }

  /* Input Styles */
  .input-container {
    width: 100%;
    min-height: 80px;
    max-height: 100px;
    flex-shrink: 0;
    box-sizing: border-box;
  }

  .input-wrapper {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-height: 64px;
    height: 90px;
    padding: 5px;
    gap: 12px;
    background: rgba(0, 0, 0, 0.4); 
    backdrop-filter: blur(10px); 
    border: 1px solid rgba(255, 255, 255, 0.18);
    border-radius: 22px;
    box-sizing: border-box;
  }

  .message-input {
    flex: 1;
    width: 100%;
    min-height: 16px;
    height: 34px;
    padding: 8px 10px;
    background: none;
    border: none;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 400;
    line-height: 16px;
    letter-spacing: -0.01em;
    resize: none;
    outline: none;
    box-sizing: border-box;
  }

  .message-input::placeholder {
    color: rgba(255, 255, 255, 0.5);
  }

  .input-actions {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
  }

  .input-actions-left {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .input-actions-center {
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 1;
    gap: 5px;
    max-width: 220px;
    margin: 0 auto;
  }

  .input-actions-right {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .input-action-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 28px;
    height: 28px;
    padding: 6px;
    background: none;
    border: none;
    border-radius: 6px;
    color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .input-action-btn:hover {
    background: rgba(255, 255, 255, 0.08);
    color: rgba(255, 255, 255, 0.8);
  }

  .mode-btn {
    height: 30px;
    padding: 0 12px;
    background: rgba(255, 255, 255, 0.15); 
    backdrop-filter: blur(8px); 
    border: 1px solid rgba(255, 255, 255, 0.22);
    border-radius: 15px;
    color: rgba(255, 255, 255, 0.95);
    font-family: Poppins, sans-serif;
    font-size: 10px;
    font-weight: 500;
    line-height: 14px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .mode-btn:hover {
    background: rgba(255, 255, 255, 0.22);
    border-color: rgba(255, 255, 255, 0.35);
  }

  .avatar-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    background: none;
    border: none;
    cursor: pointer;
  }

  .avatar {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 34px;
    height: 34px;
    background: #2563eb;
    border: 2px solid rgba(255, 255, 255, 0.15);
    border-radius: 42px;
    backdrop-filter: blur(8px);
    transition: all 0.2s ease;
  }

  .avatar:hover {
    transform: scale(1.05);
    border-color: rgba(255, 255, 255, 0.25);
  }

  /* Responsiveness */
  @media (max-width: 1200px) {
    .app-container {
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
    }

    .main-content {
      padding: 16px 24px;
    }
  }

  @media (max-width: 900px) {
    .app-container {
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
    }

    .sidebar {
      width: 220px;
      min-width: 220px;
    }

    .main-content {
      padding: 16px 20px;
    }

    .message-title {
      font-size: 14px;
      line-height: 18px;
    }
  }

  @media (max-width: 768px) {
    .app-container {
      flex-direction: column;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      border-radius: 0;
    }

    .sidebar {
      width: 100%;
      height: auto;
      max-height: 140px;
      padding: 12px;
      border-right: none;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      border-top-left-radius: 0;
      border-top-right-radius: 0;
      border-bottom-left-radius: 0;
    }

    .topside {
      flex-direction: row;
      gap: 8px;
      padding-bottom: 8px;
      margin-bottom: 8px;
    }

    .new-chat-btn,
    .search-container {
      flex: 1;
      height: 32px;
    }

    .chat-history,
    .chat-history-header {
      display: none;
    }

    .main-content {
      flex: 1;
      padding: 12px;
      gap: 12px;
      border-top-right-radius: 0;
      border-bottom-right-radius: 0;
      border-bottom-left-radius: 0;
    }

    .message-title {
      font-size: 14px;
      line-height: 16px;
    }

    .message-text {
      font-size: 11px;
    }

    .input-container {
      min-height: 80px;
    }

    .input-wrapper {
      height: 64px;
    }
  }

  @media (max-width: 640px) {
    .mode-btn {
      font-size: 8px;
      height: 24px;
      padding: 0 6px;
      border-radius: 10px;
    }

    .input-actions-center {
      gap: 3px;
      max-width: 160px;
    }

    .user-message {
      max-width: 220px;
    }
  }

  @media (max-width: 480px) {
    .app-container {
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
    }

    .main-content {
      padding: 8px;
    }

    .sidebar {
      padding: 8px;
    }

    .message-content {
      padding: 12px;
    }

    .message-title {
      font-size: 12px;
      line-height: 14px;
    }

    .message-text {
      font-size: 10px;
      line-height: 14px;
    }

    .input-actions-center {
      flex-direction: column;
      gap: 3px;
      max-width: 100px;
    }

    .mode-btn {
      font-size: 7px;
      height: 20px;
      padding: 0 5px;
    }
  }
</style>
