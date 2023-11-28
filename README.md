# tezos-smart-contract-interaction-Using-SmartPy- 
This script defines a simple smart contract using SmartPy with two entry points: increment and decrement. The test_smart_contract_interaction function tests the smart contract by deploying it and interacting with its entry points. 
from smartpy import sp

class MySmartContract(sp.Contract):
    def __init__(self):
        self.init(storage=sp.int(0))

    @sp.entry_point
    def increment(self, params):
        self.data.storage += 1

    @sp.entry_point
    def decrement(self, params):
        self.data.storage -= 1

@sp.add_test(name="Test Smart Contract Interaction")
def test_smart_contract_interaction():
    # Deploy the smart contract
    my_contract = MySmartContract()

    scenario = sp.test_scenario()
    scenario += my_contract

    # Interact with the smart contract
    scenario.h1("Smart Contract Interaction")
    scenario += my_contract.increment()
    scenario.verify(my_contract.data.storage == 1, "Increment operation failed")

    scenario += my_contract.decrement()
    scenario.verify(my_contract.data.storage == 0, "Decrement operation failed")

if __name__ == "__main__":
    test_smart_contract_interaction()
