# Full-Stack-Blockchain-
Develop blockchain on Double zero solution which 100x faster than traditional blockchain. That has its own fiber links.
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/access/Ownable.sol";

contract DoubleZeroData is Ownable {
    string public networkStatus;
    uint256 public constant FAST_LANE_FEE = 0.01 ether;

    event StatusUpdated(string newStatus, address updater);

    constructor() Ownable(msg.sender) {
        networkStatus = "DoubleZero Nodes Online";
    }

    // A function to update status, simulating a high-speed data feed
    function updateStatus(string memory _status) public payable {
        require(msg.value >= FAST_LANE_FEE, "Insufficient 2Z/ETH for high-speed routing");
        networkStatus = _status;
        emit StatusUpdated(_status, msg.sender);
    }

    function withdraw() external onlyOwner {
        payable(owner()).transfer(address(this).balance);
    }
}

