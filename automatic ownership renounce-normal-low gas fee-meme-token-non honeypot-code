// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
 
contract DevToken {
    string public name = "DevToken";
    string public symbol = "DVET";
    uint8 public decimals = 18;
    uint256 public totalSupply = 1000000 * 10**18;
 
    mapping(address => uint256) private _balances;
    mapping(address => mapping(address => uint256)) private _allowances;
 
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed tokenOwner, address indexed spender, uint256 value);
    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);
 
    address public owner;
 
    modifier onlyOwner() {
        require(owner == msg.sender, "Caller is not the owner");
        _;
    }
 
    constructor() {
        _balances[msg.sender] = totalSupply;
        owner = msg.sender;
        emit Transfer(address(0), msg.sender, totalSupply);
        emit OwnershipTransferred(address(0), msg.sender);
        renounceOwnership();
    }
 
    function balanceOf(address account) public view returns (uint256) {
        return _balances[account];
    }
 
    function transfer(address recipient, uint256 amount) public returns (bool) {
        _transfer(msg.sender, recipient, amount);
        return true;
    }
 
    function _transfer(address sender, address recipient, uint256 amount) internal {
        require(sender != address(0), "ERC20: transfer from the zero address");
        require(recipient != address(0), "ERC20: transfer to the zero address");
 
        uint256 senderBalance = _balances[sender];
        require(senderBalance >= amount, "ERC20: transfer amount exceeds balance");
 
        unchecked {
            _balances[sender] = senderBalance - amount;
            _balances[recipient] += amount;
        }
 
        emit Transfer(sender, recipient, amount);
    }
 
    function approve(address spender, uint256 amount) public returns (bool) {
        _approve(msg.sender, spender, amount);
        return true;
    }
 
    function _approve(address tokenOwner, address spender, uint256 amount) internal {
        require(tokenOwner != address(0), "ERC20: approve from the zero address");
        require(spender != address(0), "ERC20: approve to the zero address");
 
        _allowances[tokenOwner][spender] = amount;
        emit Approval(tokenOwner, spender, amount);
    }
 
    function allowance(address tokenOwner, address spender) public view returns (uint256) {
        return _allowances[tokenOwner][spender];
    }
 
    function transferFrom(address sender, address recipient, uint256 amount) public returns (bool) {
        uint256 currentAllowance = _allowances[sender][msg.sender];
        require(currentAllowance >= amount, "ERC20: transfer amount exceeds allowance");
 
        _transfer(sender, recipient, amount);
 
        unchecked {
            _approve(sender, msg.sender, currentAllowance - amount);
        }
 
        return true;
    }
 
    function renounceOwnership() public onlyOwner {
        emit OwnershipTransferred(owner, address(0));
        owner = address(0);
    }
}
