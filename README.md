# Create-Defi-Dapp-Ethereum 
pragma solidity ^0.6.0;

contract Lending {
    // Declare mapping to store users' balances
    mapping(address => uint) public balances;

    // Declare events for logging
    event Lend(address lender, uint amount);
    event Borrow(address borrower, uint amount);
    event Repay(address borrower, uint amount);

    // Function to allow users to lend Ether
    function lend(uint amount) public {
        require(msg.value == amount, "Invalid amount");
        balances[msg.sender] += amount;
        emit Lend(msg.sender, amount);
    }

    // Function to allow users to borrow Ether
    function borrow(uint amount) public {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        msg.sender.transfer(amount);
        emit Borrow(msg.sender, amount);
    }

    // Function to allow users to repay borrowed Ether
    function repay(uint amount) public {
        require(msg.value == amount, "Invalid amount");
        balances[msg.sender] += amount;
        emit Repay(msg.sender, amount);
    }
}
