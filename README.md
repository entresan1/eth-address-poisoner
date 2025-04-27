# ✨ EtherEcho ✨ - Advanced ETH Address Poisoning Simulation Tool

<p align="center">
  <img src="https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/assets/logo_placeholder.png" alt="EtherEcho Logo" width="200"/>
  <br/>
  <i>Simulating Address Poisoning Attacks for Security Awareness & Research</i>
  <br/>
  <br/>
  <img src="https://img.shields.io/badge/Version-1.0.0-blue?style=for-the-badge" alt="Version">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License">
  <img src="https://img.shields.io/badge/Python-3.8+-orange?style=for-the-badge" alt="Python Version">
  <img src="https://img.shields.io/badge/Status-Active%20Development-brightgreen?style=for-the-badge" alt="Status">
  <br/>
  <img src="https://img.shields.io/github/stars/YOUR_USERNAME/YOUR_REPO?style=social" alt="GitHub Stars">
  <img src="https://img.shields.io/github/forks/YOUR_USERNAME/YOUR_REPO?style=social" alt="GitHub Forks">
</p>

---

<p align="center">
  <a href="#%EF%B8%8F-warning">⚠️ Warning</a> •
  <a href="#-what-is-eth-address-poisoning">🤔 What is Poisoning?</a> •
  <a href="#-how-etherecho-works">⚙️ How EtherEcho Works</a> •
  <a href="#-key-features">🚀 Key Features</a> •
  <a href="#-installation">🛠️ Installation</a> •
  <a href="#-usage">💡 Usage</a> •
  <a href="#-demo">🎬 Demo</a> •
  <a href="#-contributing">🤝 Contributing</a> •
  <a href="#-license">📄 License</a>
</p>

---

## ⚠️ Warning: Use Responsibly & Ethically! ⚠️

This tool is designed **strictly for educational purposes and authorized security research**. ETH Address Poisoning is a deceptive technique that can cause significant financial loss if used maliciously.

*   🛑 **DO NOT** use this tool against any individual or entity without their explicit, written permission.
*   ⚖️ Unauthorized use is **illegal and unethical**. You are solely responsible for your actions.
*   🛡️ The primary goal is to **understand the attack vector** to build better defenses and raise user awareness.
*   🎓 Use this tool to learn, test your own security assumptions (on testnets or with owned addresses), or during authorized penetration testing engagements.

**The developers assume NO liability and are NOT responsible for any misuse or damage caused by this tool.**

---

## 🤔 What is ETH Address Poisoning?

ETH Address Poisoning is a social engineering attack targeting cryptocurrency users. It exploits the common habit of users copying addresses from their transaction history rather than verifying them fully each time.

**Here's the attack flow:**

1.  **Target Identification:** The attacker identifies a target address (Victim).
2.  **Vanity Address Generation:** The attacker generates a large number of Ethereum addresses (`AttackerVanityAddr`) that visually mimic the Victim's address (or an address the Victim frequently interacts with). Usually, the first few and last few characters match (e.g., `0x1234...abcd`).
3.  **The "Poison" Transaction:** The attacker sends a tiny (often zero-value) amount of ETH or a token *from* their `AttackerVanityAddr` *to* the Victim's address.
4.  **The Trap:** This transaction now appears in the Victim's wallet history. The `AttackerVanityAddr` looks very similar to an address the Victim trusts or uses often.
5.  **The Mistake:** Later, when the Victim intends to send a *significant* amount of funds to their intended recipient, they might quickly glance at their history, see the familiar-looking `AttackerVanityAddr`, copy it, and paste it into the recipient field without careful verification.
6.  **Funds Lost:** The Victim unknowingly sends their funds to the attacker's vanity address instead of the legitimate recipient.

**Why it's effective:**

*   **User Habit:** Relies on the shortcut of copy-pasting from history.
*   **Visual Deception:** Long hexadecimal addresses are hard to compare character-by-character. Matching start/end characters often provide a false sense of security.
*   **Wallet UI:** Some wallets truncate addresses in the UI, making the similar parts more prominent.

---

## ⚙️ How EtherEcho Works

`EtherEcho` automates the crucial steps of an address poisoning *simulation* for security testing:

1.  **🎯 Input:** You provide the target address you want to simulate the attack against (e.g., an address you own on a testnet for research). Optionally, you can provide addresses the target frequently interacts with (counterparties) to generate even more deceptive vanity addresses.
2.  **🔑 Vanity Address Generation:** `EtherEcho` utilizes efficient algorithms [Mention specific method if applicable, e.g., multi-threaded CPU or GPU generation] to generate vanity addresses that match the first `N` and last `M` characters of the target address *or* its counterparties.
3.  **💸 Transaction Crafting:** It connects to an Ethereum node (via RPC URL) using a provided private key (which needs a small amount of ETH for gas).
4.  **☣️ Poisoning Simulation:** For each generated vanity address, it sends a minimal (configurable, near-zero) value ETH transaction *from* the vanity address *to* the target address. This populates the target's transaction history with these look-alike addresses.
5.  **📊 Logging & Output:** Provides clear logs of generated addresses, transaction hashes, and success/failure status.

```mermaid
graph LR
    A[Provide Target Address & Config] --> B(EtherEcho Tool);
    B --> C{Generate Vanity Addresses <br/> (Matching Start/End)};
    C --> D[Fund Vanity Addresses (Internal Step/Requires Pre-funded Source)];
    D --> E{Craft Tiny TX <br/> (From Vanity -> Target)};
    E --> F[Send TX via RPC];
    F --> G[Target History Poisoned <br/> (Simulation Complete)];
    G --> H(Log Results / TX Hashes);

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#ccf,stroke:#333,stroke-width:2px
    style G fill:#f9d,stroke:#333,stroke-width:2px
    style H fill:#9cf,stroke:#333,stroke-width:2px

🚀 Key Features: Why EtherEcho Stands Out

✨ High-Performance Generation: Optimized vanity address generation [mention specifics like 'multi-core support' or 'GPU acceleration via XYZ' if true]. Find matching addresses faster.

🎯 Advanced Targeting: Poison based on the target or their frequent counterparties for more realistic simulation scenarios.

🔧 Highly Configurable:

Set custom prefix/suffix lengths for vanity addresses.

Adjust the tiny ETH value sent in poisoning transactions.

Configure gas price/limit settings.

Specify custom RPC endpoints (Mainnet, Testnets, Local).

🌐 Network Flexibility: Works with any EVM-compatible chain via RPC (Ethereum Mainnet, Goerli, Sepolia, Polygon, BSC, etc.).

🔐 Security Focused: Designed for researchers and blue teams to understand and test defenses. Does not store private keys persistently [Verify this is true for your tool].

📈 Clear Logging: Verbose output detailing the process, generated addresses, and transaction hashes for analysis.

🐍 Clean Python Codebase: Easy to understand, modify, and contribute to.

🛠️ Installation

Clone the Repository:

git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Install Dependencies:

pip install -r requirements.txt
# Or using Poetry: poetry install
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Configuration:

Copy the example configuration file: cp config.example.yaml config.yaml

Edit config.yaml with your details:

rpc_url: Your Ethereum node RPC endpoint (e.g., Infura, Alchemy, or a local node).

private_key: !! DANGER !! The private key of the source wallet used to fund the temporary vanity addresses and pay for gas. Use a dedicated burner wallet with minimal funds ONLY for testing/research. Consider using environment variables for better security (see below).

value_to_send_ether: The tiny amount of ETH to send in each poisoning transaction (e.g., "0.00001").

Security Best Practice: Avoid storing private keys directly in config files. Use environment variables:

export ETHERECHO_PRIVATE_KEY="0xYourPrivateKeyHere"
export ETHERECHO_RPC_URL="https://mainnet.infura.io/v3/YOUR_INFURA_ID"
# Then modify the script to read from os.environ
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END
💡 Usage

Basic Poisoning Simulation:

python etherecho.py --target 0xVictimAddress TARGET_ADDRESS --prefix 5 --suffix 4 --count 10
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Explanation:

--target TARGET_ADDRESS: The ETH address to simulate poisoning against (e.g., 0xAb5801a7D398351b8bE11C439e05C5B3259aeC9B).

--prefix N: Match the first N characters (after 0x).

--suffix M: Match the last M characters.

--count C: Generate C different vanity addresses and send transactions.

Targeting Counterparties:

python etherecho.py --target 0xVictimAddress \
                    --counterparties 0xCounterParty1 0xCounterParty2 \
                    --prefix 6 --suffix 5 --count 20 \
                    --value 0.000001 --gas-price 30
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

--counterparties ADDR1 ADDR2 ...: Generate addresses matching these as well as the main target.

--value ETHER: Override the config file value for the amount sent.

--gas-price GWEI: Set a specific gas price in Gwei.

See Full Options:

python etherecho.py --help
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END
🎬 Demo

(Optional: Create a short GIF or video demonstrating the tool's setup and execution, especially the transaction appearing in a block explorer or wallet history on a testnet. Upload it to the repo and link it here.)

![EtherEcho Demo GIF](https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/assets/etherecho_demo.gif)
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Markdown
IGNORE_WHEN_COPYING_END

(Placeholder: A brief description of what the demo shows)
This demo showcases EtherEcho generating a vanity address matching the first 5 and last 4 characters of a target address on the Sepolia testnet and sending a 0.00001 ETH transaction. You can see the generated address and the successful transaction hash in the output.

🤝 Contributing

Contributions are welcome! If you have ideas for improvements, bug fixes, or new features:

Fork the repository.

Create a new branch: git checkout -b feature/your-feature-name or bugfix/issue-description.

Make your changes.

Add tests for your changes if applicable.

Ensure your code lints (flake8, black).

Commit your changes: git commit -m "feat: Add amazing new feature"

Push to the branch: git push origin feature/your-feature-name

Open a Pull Request with a clear description of your changes.

Please adhere to the project's code of conduct (if you add one).

📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

Remember, with great power comes great responsibility. Use this tool ethically.

IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END
