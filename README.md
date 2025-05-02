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

ElizaOS utilizes the Hedera network for [**Explain the primary use case of Hedera here, e.g., secure and transparent logging of agent actions, decentralized identity management, verifiable data storage**]. This provides immutability and trust for critical agent operations.

You can see how Hedera is integrated within the ElizaOS codebase in the following location:

```typescript
// agent/src/index.ts
import { /* Hedera related classes/functions */ } from './lib/hedera';

class AgentRuntime {
  async performAction(action: Action) {
    // ... agent logic ...
    const transactionId = await hederaService.logAction(action);
    console.log(`Action logged on Hedera with transaction ID: ${transactionId}`);
    // ... more agent logic ...
  }
}
```
In the agent/src/index.ts file, the AgentRuntime class demonstrates how the hederaService (which would be an abstraction over the Hedera SDK) is used to log agent actions on the Hedera network. This ensures a verifiable and tamper-proof record of the agent's activities. [Adjust the file path and code snippet to accurately reflect your Hedera usage.]

HIP-991 and/or HCS-10 Usage
[Choose the relevant section based on which HIP you've implemented or if you've implemented HCS-10.]

HIP-991: Account Association
ElizaOS leverages HIP-991 for [Explain how you are using Account Association, e.g., allowing users to associate their Hedera accounts with their agent instances for enhanced control and ownership]. This feature enables a more direct and secure interaction between users and their agents on the Hedera network.

The code demonstrating the usage of HIP-991 can be found here:

```TypeScript

// client/src/lib/api.ts
export async function associateAccount(agentId: string, accountId: string) {
  const response = await fetch('/api/hedera/associate', {
    method: 'POST',
    body: JSON.stringify({ agentId, accountId }),
    headers: { 'Content-Type': 'application/json' },
  });
  // ... handle response ...
}
```
The associateAccount function in client/src/lib/api.ts shows an example of how the frontend interacts with the backend to initiate the account association process as defined by HIP-991. [Adjust the file path and code snippet accordingly.]

HCS-10: Decentralized Topic Messaging
ElizaOS utilizes HCS-10 to enable [Explain how you are using HCS-10, e.g., real-time communication between agents and users, broadcasting events within the ElizaOS ecosystem in a decentralized manner]. This allows for secure, ordered, and tamper-proof messaging between different components of the ElizaOS platform.

Here's an example of how HCS-10 is used in the backend:

```TypeScript

// agent/src/services/hcsService.ts (This is a hypothetical path, adjust to your actual path)
import { /* HCS related classes/functions */ } from '@hashgraph/sdk';

class HCSService {
  topicId: TopicId;
  client: Client;

  constructor() {
    this.topicId = TopicId.fromString(process.env.HCS_TOPIC_ID!);
    this.client = Hedera.getClient();
  }

  async sendMessage(message: string) {
    const submitTransaction = await new TopicMessageSubmitTransaction({
      topicId: this.topicId,
      message: message,
    }).execute(this.client);
    const receipt = await submitTransaction.getReceipt(this.client);
    console.log(`HCS message submitted with receipt: ${receipt.status}`);
  }
}
```
The HCSService (in a hypothetical agent/src/services/hcsService.ts file) illustrates how the Hedera Consensus Service (HCS-10) is used to send messages to a specific topic. This allows for decentralized and auditable communication within the ElizaOS platform. [Make sure to replace the hypothetical file path and code with your actual implementation.]






## 🤝 Contributing

Contributions are welcome! Please refer to the CONTRIBUTING.md file for guidelines.

## 📜 License

This project is licensed under the MIT License. See the LICENSE file for details.
