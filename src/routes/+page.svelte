<script>
  import { onMount } from "svelte";

  let searchQuery = "";
  let messageInput = "";
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
</script>

<div class="app-header"></div>
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
        <div class="chat-item" class:active={index === 0}>
          <span class="chat-title">{chat}</span>
          {#if index === 3}
            <div class="more-btn">
              <img src="/Vector.svg" alt="" />
            </div>
          {/if}
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
  }

  :global(*::-webkit-scrollbar) {
    display: none;
  }

  /* Background */
  .app-header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-image: url("/background.jpg");
    background-size: cover;
    background-position: center;
    z-index: -3;
    pointer-events: none;
  }

  /* Main Container */
  .app-container {
    position: fixed;
    top: 10px;
    left: 10px;
    width: calc(100vw - 20px);
    height: calc(100vh - 20px);
    display: flex;
    border-radius: 20px;
    background: linear-gradient(
      112.58deg,
      rgba(0, 0, 0, 0.8) 0%,
      rgba(0, 0, 0, 0.3) 100%
    );
    border: 1px solid #ffffff4d;
    backdrop-filter: blur(34px);
    font-family: Poppins, sans-serif;
    overflow: hidden;
    box-sizing: border-box;
    box-shadow:
      0 32px 64px -12px rgba(0, 0, 0, 0.4),
      inset 4px 4px 20px 0px #ffffff52;
    z-index: 1;
  }

  /* Sidebar Styles */
  .sidebar {
    display: flex;
    flex-direction: column;
    width: 333px;
    padding: 40px 20px;
    background: rgba(0, 0, 0, 0.2);
    border-right: 1px solid rgba(255, 255, 255, 0.08);
    border-top-left-radius: 20px;
    border-bottom-left-radius: 20px;
    gap: 11px;
  }

  .topside {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-bottom: 20px;
    padding-bottom: 20px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  }

  .new-chat-btn {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    height: 48px;
    padding: 0 16px;
    gap: 12px;
    background: rgba(0, 0, 0, 0.4);
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 12px;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 14px;
    font-weight: 500;
    line-height: 20px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .new-chat-btn:hover {
    background: rgba(255, 255, 255, 0.08);
    border-color: rgba(255, 255, 255, 0.2);
    color: white;
  }

  .search-container {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    height: 48px;
    padding: 0 16px;
    background: rgba(0, 0, 0, 0.4);
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 12px;
    transition: all 0.2s ease;
    box-sizing: border-box;
  }

  .search-container:hover,
  .search-container:focus-within {
    background: rgba(255, 255, 255, 0.08);
    border-color: rgba(255, 255, 255, 0.2);
  }

  .search-input {
    width: 100%;
    height: 20px;
    padding-right: 32px;
    background: none;
    border: none;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 14px;
    font-weight: 400;
    line-height: 20px;
    letter-spacing: -0.01em;
    outline: none;
  }

  .search-input::placeholder {
    color: rgba(255, 255, 255, 0.5);
  }

  .search-btn {
    position: absolute;
    right: 16px;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: none;
    color: rgb(255, 255, 255);
    cursor: pointer;
    padding: 0;
    width: 18px;
    height: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s ease;
  }

  .search-btn:hover {
    color: rgba(255, 255, 255, 0.9);
  }

  .chat-history-header {
    margin-top: 8px;
    margin-bottom: 12px;
    color: rgba(255, 255, 255, 0.5);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 500;
    line-height: 16px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .chat-history {
    display: flex;
    flex-direction: column;
    flex: 1;
    gap: 4px;
    overflow-y: auto;
  }

  .chat-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 44px;
    padding: 2px 16px;
    gap: 12px;
    background: transparent;
    border-radius: 12px;
    font-family: Poppins, sans-serif;
    font-size: 14px;
    font-weight: 400;
    line-height: 20px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .chat-item:hover {
    background: rgba(255, 255, 255, 0.05);
  }

  .chat-item.active {
    background: rgba(255, 255, 255, 0.08);
    border: 1px solid rgba(255, 255, 255, 0.12);
  }

  .chat-title {
    flex: 1;
    color: rgba(255, 255, 255, 0.8);
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .chat-item.active .chat-title {
    color: rgba(255, 255, 255, 0.95);
  }

  .more-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 28px;
    height: 28px;
    padding: 6px;
    background: none;
    border: none;
    border-radius: 8px;
    color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .more-btn:hover {
    background: rgba(255, 255, 255, 0.1);
    color: rgba(255, 255, 255, 0.8);
  }

  /* Main Content Styles */
  .main-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 20px 70px;
    gap: 33px;
    border-top-right-radius: 20px;
    border-bottom-right-radius: 20px;
    overflow: hidden;
    box-sizing: border-box;
  }

  .messages-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 24px;
    overflow-y: auto;
    overflow-x: hidden;
    min-height: 0;
    box-sizing: border-box;
  }

  .message {
    width: 100%;
  }

  .assistant-message {
    align-self: flex-start;
  }

  .user-message {
    align-self: flex-end;
    max-width: 365px;
    width: fit-content;
  }

  .message-content {
    padding: 24px;
    background: rgba(255, 255, 255, 0.08);
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 16px;
    box-sizing: border-box;
  }

  .message-title {
    margin: 0 0 16px 0;
    color: rgba(255, 255, 255, 0.95);
    font-family: Poppins, sans-serif;
    font-size: 18px;
    font-weight: 600;
    line-height: 26px;
    letter-spacing: -0.02em;
  }

  .message-text {
    margin: 0 0 20px 0;
    color: rgba(255, 255, 255, 0.8);
    font-family: Poppins, sans-serif;
    font-size: 14px;
    font-weight: 400;
    line-height: 22px;
    letter-spacing: -0.01em;
  }

  .message-actions {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;
  }

  .action-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32px;
    height: 32px;
    padding: 8px;
    background: none;
    border: none;
    border-radius: 8px;
    color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .action-btn:hover {
    background: rgba(255, 255, 255, 0.05);
    color: rgba(255, 255, 255, 0.8);
  }

  .sources-btn {
    height: 36px;
    padding: 0 16px;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.15);
    border-radius: 18px;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 500;
    line-height: 16px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .sources-btn:hover {
    background: rgba(255, 255, 255, 0.15);
    border-color: rgba(255, 255, 255, 0.25);
  }

  .user-message-content {
    padding: 14px;
    background: #2563eb99;
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 20px;
    color: rgba(255, 255, 255, 0.95);
    font-family: Poppins, sans-serif;
    font-size: 14px;
    font-weight: 400;
    line-height: 20px;
    letter-spacing: -0.01em;
    box-sizing: border-box;
    overflow-wrap: break-word;
  }

  /* Input Styles */
  .input-container {
    width: 100%;
    min-height: 100px;
    max-height: 120px;
    flex-shrink: 0;
    box-sizing: border-box;
  }

  .input-wrapper {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-height: 80px;
    height: 114px;
    padding: 6px;
    gap: 14px;
    background: #00000066;
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.15);
    border-radius: 26px;
    box-sizing: border-box;
  }

  .message-input {
    flex: 1;
    width: 100%;
    min-height: 20px;
    height: 41px;
    padding: 10px 12px;
    background: none;
    border: none;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 14px;
    font-weight: 400;
    line-height: 20px;
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
    gap: 12px;
  }

  .input-actions-left {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .input-actions-center {
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 1;
    gap: 6px;
    max-width: 280px;
    margin: 0 auto;
  }

  .input-actions-right {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .input-action-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32px;
    height: 32px;
    padding: 8px;
    background: none;
    border: none;
    border-radius: 8px;
    color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .input-action-btn:hover {
    background: rgba(255, 255, 255, 0.08);
    color: rgba(255, 255, 255, 0.8);
  }

  .mode-btn {
    height: 36px;
    padding: 0 16px;
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.15);
    border-radius: 18px;
    color: rgba(255, 255, 255, 0.9);
    font-family: Poppins, sans-serif;
    font-size: 12px;
    font-weight: 500;
    line-height: 16px;
    letter-spacing: -0.01em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .mode-btn:hover {
    background: rgba(255, 255, 255, 0.15);
    border-color: rgba(255, 255, 255, 0.25);
  }

  .mode-btn:focus {
    outline: none;
    border-color: rgba(255, 255, 255, 0.3);
    box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.1);
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
    width: 40px;
    height: 40px;
    background: #2563eb;
    border: 2px solid rgba(255, 255, 255, 0.15);
    border-radius: 50px;
    backdrop-filter: blur(10px);
    transition: all 0.2s ease;
  }

  .avatar:hover {
    transform: scale(1.05);
    border-color: rgba(255, 255, 255, 0.25);
  }

  /* Responsiveness */
  @media (max-width: 1200px) {
    .app-container {
      top: 30px;
      left: 30px;
      width: calc(100vw - 60px);
      height: calc(100vh - 60px);
    }

    .main-content {
      padding: 20px 30px;
    }
  }

  @media (max-width: 900px) {
    .app-container {
      top: 20px;
      left: 20px;
      width: calc(100vw - 40px);
      height: calc(100vh - 40px);
    }

    .sidebar {
      width: 280px;
      min-width: 280px;
    }

    .main-content {
      padding: 20px 25px;
    }

    .message-title {
      font-size: 16px;
      line-height: 22px;
    }
  }

  @media (max-width: 768px) {
    .app-container {
      flex-direction: column;
      top: 10px;
      left: 10px;
      width: calc(100vw - 20px);
      height: calc(100vh - 20px);
      border-radius: 16px;
    }

    .sidebar {
      width: 100%;
      height: auto;
      max-height: 180px;
      padding: 15px;
      border-right: none;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      border-top-left-radius: 16px;
      border-top-right-radius: 16px;
      border-bottom-left-radius: 0;
    }

    .topside {
      flex-direction: row;
      gap: 10px;
      padding-bottom: 10px;
      margin-bottom: 10px;
    }

    .new-chat-btn,
    .search-container {
      flex: 1;
      height: 40px;
    }

    .chat-history,
    .chat-history-header {
      display: none;
    }

    .main-content {
      flex: 1;
      padding: 15px;
      gap: 15px;
      border-top-right-radius: 0;
      border-bottom-right-radius: 16px;
      border-bottom-left-radius: 16px;
    }

    .message-title {
      font-size: 16px;
      line-height: 20px;
    }

    .message-text {
      font-size: 13px;
    }

    .input-container {
      min-height: 100px;
    }

    .input-wrapper {
      height: 80px;
    }
  }

  @media (max-width: 640px) {
    .mode-btn {
      font-size: 10px;
      height: 28px;
      padding: 0 8px;
      border-radius: 12px;
    }

    .input-actions-center {
      gap: 4px;
      max-width: 200px;
    }

    .user-message {
      max-width: 280px;
    }
  }

  @media (max-width: 480px) {
    .app-container {
      top: 5px;
      left: 5px;
      width: calc(100vw - 10px);
      height: calc(100vh - 10px);
    }

    .main-content {
      padding: 10px;
    }

    .sidebar {
      padding: 10px;
    }

    .message-content {
      padding: 16px;
    }

    .message-title {
      font-size: 14px;
      line-height: 18px;
    }

    .message-text {
      font-size: 12px;
      line-height: 18px;
    }

    .input-actions-center {
      flex-direction: column;
      gap: 4px;
      max-width: 120px;
    }

    .mode-btn {
      font-size: 9px;
      height: 24px;
      padding: 0 6px;
    }
  }
</style>
