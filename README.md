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

ElizaOS is an open-source platform for building and deploying autonomous AI agents. It provides a flexible and modular architecture, allowing developers to create intelligent agents that can interact with the world, learn from experience, and achieve complex goals.

## Key Features

* **Modular Agent Architecture:** Design agents with composable skills and knowledge.
* **Multi-Modal Communication:** Agents can interact through text, audio, and potentially more.
* **Knowledge Management:** Robust system for storing, retrieving, and utilizing information.
* **Extensible Plugin System:** Easily add new capabilities and integrations.
* **Built with Cutting-Edge Technologies:** Leveraging modern tools for performance and scalability.



## Hedera Integration

ElizaOS utilizes the Hedera network through the `@elizaos/plugin-hedera`. This plugin empowers the `HederaHelper` agent to interact with the Hedera ledger for a variety of operations, including checking balances, transferring tokens, creating new tokens and topics, and managing consensus service messages.




## Dependency on `@elizaos/plugin-hedera`

The `@elizaos/agent` package relies on the `@elizaos/plugin-hedera` to enable interaction with the Hedera network. This dependency is declared in the `dependencies` section of the `agent/package.json` file:

```json
"dependencies": {
  // ... other dependencies ...
  "@elizaos/plugin-hedera": "github:hedera-dev/eliza-plugin-hedera#main",
  // ... other dependencies ...
}
```
This line specifies that the @elizaos/agent requires the @elizaos/plugin-hedera package. Instead of fetching it from the standard npm registry, the package manager (like npm, yarn, or pnpm) is instructed to obtain it directly from the main branch of the hedera-dev/eliza-plugin-hedera GitHub repository.

During the installation process (npm install, yarn install, pnpm install), the package manager will:

Access the specified GitHub repository.
Download the code from the main branch of the @elizaos/plugin-hedera repository.
Install the plugin and its own dependencies within the node_modules directory of the @elizaos/agent package.
Once installed, the @elizaos/agent code can import and utilize the functionalities provided by the @elizaos/plugin-hedera, as demonstrated in agent/src/defaultCharacter.ts:

```TypeScript

import { hederaPlugin } from '@elizaos/plugin-hedera';
```
This import statement makes the Hedera plugin's modules and functions available for use within the agent's logic, enabling features like interacting with the Hedera Consensus Service.




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

 HIP-991: Permissionless Revenue-Generating Topic IDs (Potential Future Use)

HIP-991 introduces permissionless revenue-generating Topic IDs to the Hedera Consensus Service (HCS). This enhancement allows topic operators to set optional fixed fees for message submissions, enabling new monetization strategies and enhanced access control. Fees can be denominated in HBAR or any Hedera Token Service (HTS) fungible token, and can be distributed to multiple wallets. A Fee Exempt Key List allows authorized entities to submit messages without paying fees.

While the current `HederaHelper` agent (defined in `agent/src/defaultCharacter.ts`) demonstrates the creation and submission of messages to HCS topics, it doesn't yet explicitly showcase the revenue-generating features introduced by HIP-991.

However, the architecture of ElizaOS and the `hederaPlugin` make it well-positioned to leverage these capabilities in the future. For example, the `HederaHelper` could be extended to:

* **Create topics with custom fees:** Allowing the agent operator to earn HBAR or HTS tokens for each message submitted to a specific topic.
* **Implement fee-based access to agent functionalities:** By requiring a small HBAR or HTS token fee to interact with certain commands or access premium information disseminated through an HCS topic.
* **Manage Fee Exempt Key Lists:** Granting specific user accounts or other agents free access to certain topics or functionalities.

The `messageExamples` in `agent/src/defaultCharacter.ts` already show the agent interacting with HCS topics:

```typescript
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
