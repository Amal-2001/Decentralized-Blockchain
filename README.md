# Decentralized Blockchain 
 

//pragma solidity >=0.7.0 <0.9.0;
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
contract Token {
   mapping(address => uint256) balances;
   mapping(address => mapping (address => uint256)) allowed;
   string name_;
   string symbol_;
   uint256 totalSupply_;
   constructor(string memory _name, string memory _symbol, uint256 _total) {
      name_ = _name;
      symbol_ = _symbol;
      totalSupply_ = _total;
      balances[msg.sender] = totalSupply_;
   }
   
   function name() public view returns (string memory) {
      return name_;
   }
   function symbol() public view returns (string memory) {
      return symbol_;
   }
   function totalSupply() public view returns (uint256) {
      return totalSupply_;
   }
   function balanceOf(address tokenOwner) public view returns (uint) {
      return balances[tokenOwner];
   }
   function decimals() public pure returns(uint8) {
      return 18;
   }
   function transfer(address _receiver, uint _amount) public returns (bool) {
      require(_amount <= balances[msg.sender]);
      balances[msg.sender] -= _amount;
      balances[_receiver] += _amount;
      return true;
   }
   function approve(address _delegate, uint _amount) public returns (bool) {
      allowed[msg.sender][_delegate] = _amount;
      return true;
   }
   function allowance(address _owner, address _delegate) public view returns (uint) {
      return allowed[_owner][_delegate];
   }
   function transferFrom(address _owner, address _receiver, uint _amount) public returns (bool) {
      require(_amount <= balances[_owner]);
      require(_amount <= allowed[_owner][msg.sender]);          
      balances[_owner] -= _amount;
      allowed[_owner][msg.sender] -= _amount;
      balances[_receiver] += _amount;
      return true; 
   }
}
// // Smart Contract for the Voting application
// contract VotingForTopper {

// 	// Refer to the owner
// 	address owner;

// 	// Declaring the public variable 'purpose'
// 	// to demonstrate the purpose of voting
// 	string public purpose;
	
// 	// Defining a structure with boolean
// 	// variables authorized and voted
// 	struct Voter{
// 		bool authorized;
// 		bool voted;
// 	}

// 	// Declaring the unsigned integer
// 	// variables totalVotes, and for the
// 	//3 teams- A,B, and C
// 	uint totalVotes;
// 	uint teamA;
// 	uint teamB;
// 	uint teamC;
	
// 	// Creating a mapping for the total Votes
// 	mapping(address=>Voter) info;

// 	// Defining a constructor indicating
// 	// the purpose of voting
// 	public constructor(
// 	string memory _name) public{
// 		purpose = _name;
// 		owner = msg.sender;
// 	}
	
// 	// Defining a modifier to
// 	// verify the ownership
// 	modifier ownerOn() {
// 		require(msg.sender==owner);
// 		_;
// 	}
	
// 	// Defining a function to verify
// 	// the person is voted or not
// 	function authorize(
// 	address _person) ownerOn public {
// 		info[_person].authorized= true;
		
// 	}
	
// 	// Defining a function to check and
// 	// skip the code if the person is already
// 	// voted else allow to vote and
// 	// calculate totalvotes for team A
// 	function temaAF(address _address) public {
// 		require(
// 		!info[_address].voted,
// 		"already voted person");
// 		require(
// 		info[_address].authorized,
// 		"You Have No Right for Vote");
// 		info[_address].voted = true;
// 		teamA++;
// 		totalVotes++;
// 	}


// 	function temaBF(address _address) public {
// 	require(
// 	!info[_address].voted,
// 	"already voted person");
// 		require(
// 		info[_address].authorized,
// 		"You Have No Right for Vote");
// 		teamB++;
// 		info[_address].voted = true;
// 		totalVotes++;
// 	}

// 	// Defining a function to check
// 	// and skip the code if the person
// 	// is already voted else allow to vote
// 	// and calculate totalvotes for team C
// 	function temaCF(address _address) public returns(
// 	string memory){
// 		require(
// 		!info[_address].voted,
// 		"already voted person");
// 		require(
// 		info[_address].authorized,
// 		"You Have No Right for Vote");
// 		info[_address].voted = true;
// 		teamC++;
// 		totalVotes++;
// 		return("Thanks for Voting");
// 	}

// 	function totalVotesF() public view returns(uint){
// 		return totalVotes;
// 	}


// 	function resultOfVoting() public view returns(
// 	string memory){
// 		if(teamA>teamB){
// 			if(teamA>teamC){
// 				return"A is Winning";
// 			}
// 			else if(teamC>teamA){
// 				return "C is Winning"; } }
// 		else if(teamB>teamC) {
// 			return "B is Winning";
// 		}
// 		else if(
// 		teamA==teamB && teamA==teamC || teamB==teamC ){
// 			return "No One is Winning";
// 		}
// 	}
// 	}


