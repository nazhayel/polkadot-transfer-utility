# polkadot-transfer-utility    
The polkadot-transfer-utility script simplifies the process of transferring DOT tokens on the Polkadot blockchain, providing a user-friendly interface for users to send transactions

from substrateinterface import SubstrateInterface, Keypair

class PolkadotTransferUtility:
    def __init__(self, node_url, keypair):
        self.substrate = SubstrateInterface(url=node_url)
        self.keypair = keypair

    def transfer_tokens(self, recipient, amount):
        # Initiate a DOT transfer to the specified recipient
        call = self.substrate.compose_call(
            call_module='Balances',
            call_function='transfer',
            call_params={'dest': recipient, 'value': amount}
        )
        extrinsic = self.substrate.create_signed_extrinsic(call=call, keypair=self.keypair)
        self.substrate.submit_extrinsic(extrinsic, wait_for_inclusion=True)
        print(f"{amount} DOT successfully transferred to {recipient}")

# Example Usage
node_url = "wss://rpc.polkadot.io"
alice_keypair = Keypair.create_from_mnemonic("your_alice_mnemonic_here")

transfer_utility = PolkadotTransferUtility(node_url, alice_keypair)

# Transfer DOT tokens
transfer_utility.transfer_tokens("recipient_address_here", 30)

This script offers a straightforward utility for users to transfer DOT tokens on the Polkadot blockchain. By specifying the recipient address and the amount, users can easily initiate transactions. The polkadot-transfer-utility script is designed for simplicity, making it accessible for individuals looking to perform quick and secure token transfers within the Polkadot network.
