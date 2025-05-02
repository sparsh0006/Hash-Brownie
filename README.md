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

2. Install dependencies:

   ```bash
   pnpm install
   ```

3. Set up the environment variables:

   ```bash
   cp .env.example .env
   ```
4. Add your model provider api key in the env  
   
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

- **Account Management**: Create and manage Hedera accounts.
- **Token Transactions**: Interact with Hedera tokens for payments and transfers.
- **Smart Contract Execution**: Deploy and call smart contracts on the Hedera network.


## 🤝 Contributing

Contributions are welcome! Please refer to the CONTRIBUTING.md file for guidelines.

## 📜 License

This project is licensed under the MIT License. See the LICENSE file for details.
