# Eliza 🤖

Eliza is a multi-agent simulation framework designed to create intelligent, autonomous agents with a focus on leveraging the Hedera network for secure and scalable operations. This repository is part of the Hedera AI and agents workshop.

## 🚀 Features

- **Hedera Integration**: Seamlessly interact with Hedera's decentralized network using the `@elizaos/plugin-hedera` plugin.
- **Extensible Plugins**: Add custom functionality to agents with a modular plugin system.
- **Telegram Client Support**: Enable agent communication via Telegram.


## 📂 Project Structure

- **`agent/`**: Contains the core logic for agent simulation.
- **`plugins/`**: Extendable plugins, including the Hedera integration plugin.
- **`docs/`**: Documentation and guides for the project.

## 🛠️ Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/hedera-dev/hedera-ai-agent-workshop.git
   cd hedera-ai-agent-workshop
   ```

2. Move to the eliza directory 

    ```bash
    cd eliza
    ```   

3. Install dependencies:

   ```bash
   pnpm install
   ```

4. Set up the environment variables:

   ```bash
   cp .env.example .env
   ```
5. Add your model provider api key in the env  
   
   ```bash
   OPENAI_API_KEY=your_openai_api_key
   ```

## ▶️ Usage

### Start the Agent

Move to the eliza directory 

```bash
cd eliza
```

To start the agent, run:

```bash
pnpm start
```

### Development Mode

Move to the eliza directory 

```bash
cd eliza
```

For live development with file watching:

```bash
pnpm run dev
```

### Run Tests

To execute the test suite:

```bash
pnpm test
```

## 📦 Hedera Plugin

The `@elizaos/plugin-hedera` plugin enables seamless integration with the Hedera network. It provides the following features:

### Hedera Token Service (HTS)
- **Create Tokens**: Create fungible and non-fungible tokens with customizable parameters
- **Mint Tokens**: Add supply to existing tokens
- **Transfer Tokens**: Move tokens between accounts
- **Associate/Dissociate Tokens**: Manage token relationships with accounts
- **Token Operations**: Reject tokens, query balances, retrieve token holder information

### Hedera Consensus Service (HCS)
- **Topic Management**: Create, delete, and manage topics
- **Message Submission**: Send messages to topics
- **Information Retrieval**: Fetch topic information and messages with time-based filtering

### HBAR Operations
- **Transfer HBAR**: Send HBAR between accounts
- **Balance Queries**: Check account balances

### Airdrop Management
- **Distribute Tokens**: Airdrop tokens to multiple recipients
- **Claim Airdrops**: Retrieve pending airdrops
- **Query Pending Airdrops**: View available airdrops for accounts







# ElizaOS - Your Autonomous AI Agent Platform

[![CI](...)](...)
[![CodeQL](...)](...)
[![License](...)](LICENSE)

ElizaOS is an open-source platform for building and deploying autonomous AI agents. It provides a flexible and modular architecture, allowing developers to create intelligent agents that can interact with the world, learn from experience, and achieve complex goals.

## Key Features

* **Modular Agent Architecture:** Design agents with composable skills and knowledge.
* **Multi-Modal Communication:** Agents can interact through text, audio, and potentially more.
* **Knowledge Management:** Robust system for storing, retrieving, and utilizing information.
* **Extensible Plugin System:** Easily add new capabilities and integrations.
* **Built with Cutting-Edge Technologies:** Leveraging modern tools for performance and scalability.



## Hedera Integration

ElizaOS utilizes the Hedera network through the `@elizaos/plugin-hedera`. This plugin empowers the `HederaHelper` agent to interact with the Hedera ledger for a variety of operations, including checking balances, transferring tokens, creating new tokens and topics, and managing consensus service messages.

The `HederaHelper` character, defined in `agent/src/defaultCharacter.ts` (as shown below), explicitly includes the `hederaPlugin` in its configuration:

```typescript
// agent/src/defaultCharacter.ts
import { type Character, ModelProviderName } from '@elizaos/core';
import { hederaPlugin } from '@elizaos/plugin-hedera';
import telegramClient from '@elizaos/client-telegram';

export const defaultCharacter: Character = {
  'name': 'HederaHelper',
  'username': 'hederahelper',
  "clients": [
    telegramClient,],
    // @ts-ignore
  'plugins': [hederaPlugin], // <--- Hedera Plugin Integration

  'modelProvider': ModelProviderName.OPENAI,
  'settings': {
    'secrets': {
      'key': 'YOUR_TELEGRAM_BOT_KEY', // Replace with your actual key
    },
    'voice': {
      'model': 'en_US-hfc_female-medium',
    },
  },
  'system':
    'Act as a helpful assistant specializing in Hedera Hashgraph operations. ... (rest of the system prompt) ...',
  // ... (rest of the character definition) ...
};
```
This configuration within defaultCharacter.ts demonstrates the integration of the Hedera plugin, enabling the HederaHelper agent with Hedera-specific functionalities. The system prompt further guides the agent to process user requests for interacting with the Hedera network.

The messageExamples within the same file illustrate how users can interact with the HederaHelper for various Hedera operations, implying the use of functionalities provided by the @elizaos/plugin-hedera:

```TypeScript

// agent/src/defaultCharacter.ts (Message Examples)
'messageExamples': [
  [
    {
      'user': '{{user1}}',
      'content': {
        'text': "What's my HBAR balance?",
      },
    },
    {
      'user': 'HederaHelper',
      'content': {
        'text': 'Checking your HBAR balance now.',
        'action': 'HEDERA_HBAR_BALANCE', // <--- Potential Hedera Action
      },
    },
  ],
  [
    {
      'user': '{{user1}}',
      'content': {
        'text': 'Transfer 50 HBAR to 0.0.67890',
      },
    },
    {
      'user': 'HederaHelper',
      'content': {
        'text': 'Initiating the transfer of 50 HBAR to account 0.0.67890.',
        'action': 'TRANSFER_HBAR', // <--- Potential Hedera Action
      },
    },
  ],
  // ... (other examples for token balance, transfers, creation, association, topic management) ...
],
```
These examples suggest that the @elizaos/plugin-hedera provides the underlying logic to handle actions like HEDERA_HBAR_BALANCE, TRANSFER_HBAR, HEDERA_CREATE_TOKEN, HEDERA_ASSOCIATE_TOKEN, HEDERA_CREATE_TOPIC, and HEDERA_SUBMIT_TOPIC_MESSAGE.

HIP-991 and/or HCS-10 Usage (via @elizaos/plugin-hedera)
Based on the messageExamples, the @elizaos/plugin-hedera likely handles HIP-991 for token association and HCS-10 for topic creation and message submission.

For HIP-991 (Token Association), the following messageExample demonstrates its usage:

```TypeScript

// agent/src/defaultCharacter.ts (Token Association Example)
[
  {
    'user': '{{user1}}',
    'content': {
      'text': 'Associate token 0.0.112233 with my account.',
    },
  },
  {
    'user': 'HederaHelper',
    'content': {
      'text': 'Associating token 0.0.112233 with your account.',
      'action': 'HEDERA_ASSOCIATE_TOKEN', // <--- HIP-991 Implementation via Plugin
    },
  },
],
```
This interaction indicates that the @elizaos/plugin-hedera provides the functionality to associate a token with a user's Hedera account, aligning with the principles of HIP-991.

For HCS-10 (Decentralized Topic Messaging), the following messageExamples showcase its use:

```TypeScript

// agent/src/defaultCharacter.ts (HCS-10 Examples)
[
  {
    'user': '{{user1}}',
    'content': {
      'text': "Create a topic with memo 'Project Updates'",
    },
  },
  {
    'user': 'HederaHelper',
    'content': {
      'text': "Creating a new HCS topic with memo 'Project Updates'.",
      'action': 'HEDERA_CREATE_TOPIC', // <--- HCS-10 Implementation via Plugin
    },
  },
],
[
  {
    'user': '{{user1}}',
    'content': {
      'text': "Submit message 'Meeting rescheduled' to topic 0.0.445566",
    },
  },
  {
    'user': 'HederaHelper',
    'content': {
      'text':
        "Submitting message 'Meeting rescheduled' to topic 0.0.445566.",
      'action': 'HEDERA_SUBMIT_TOPIC_MESSAGE', // <--- HCS-10 Implementation via Plugin
    },
  },
],
```
These examples clearly show the agent's ability to create new Hedera Consensus Service topics and submit messages to existing topics, demonstrating the HCS-10 capabilities likely implemented within the @elizaos/plugin-hedera.

the defaultCharacter.ts file, we can see that the @elizaos/plugin-hedera is central to enabling Hedera functionalities within the HederaHelper agent, including features related to HIP-991 and HCS-10. The plugin abstracts the underlying Hedera SDK complexities, allowing the agent to interact with the network through a more streamlined interface.
## 🤝 Contributing

Contributions are welcome! Please refer to the CONTRIBUTING.md file for guidelines.

## 📜 License

This project is licensed under the MIT License. See the LICENSE file for details.
