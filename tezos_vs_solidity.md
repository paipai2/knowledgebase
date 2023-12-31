<table>
  <tr><th>No</th><th>Description</th><th>Solidity</th><th>Tezos</th></tr>
  <tr>
    <td>1</td>
    <td>Blackhole Address</td>
    <td>
      <pre>
0x0000000000000000000000000000000000000000
      </pre>  
    </td>
    <td>
      <pre>
tz1Ke2h7sDdakHJQh8WX4Z372du1KChsksyU
      </pre>
      <small>https://forum.smartpy.io/t/zero-address-burn-address-null-address-in-tezos/97</small>
    </td>
  </tr>
  <tr>
    <td>2</td>
    <td>Struct Declaration</td>
    <td>
      <pre>
struct Nft {
  address owner;
  uint256 tokenid;
}
      </pre>
    </td>
    <td>
      <pre>
Nft:type = sp.record(owner=sp.address, tokenid=sp.nat)
      </pre>
    </td>
  </tr>
  <tr>
    <td>3</td>
    <td>Advance Block Time</td>
    <td>
      <pre>
await advanceTimeAndBlock(86400 * 1);
      </pre>
    </td>
    <td>
      <pre>
# within test module        
scenario += c1.ep().run(now = sp.timestamp(100))
      </pre>
      <small>https://smartpy.io/manual/scenarios/testing_contracts#calls-optional-arguments</small>
    </td>
  </tr>

  <tr>
    <td>4</td>
    <td>msg.sender</td>
    <td>
      <pre>
msg.sender
      </pre>
    </td>
    <td>
      <pre>
sp.sender
      </pre>
    </td>
  </tr>

  <tr>
    <td>5</td>
    <td>tx.origin</td>
    <td>
      <pre>
tx.origin
      </pre>
    </td>
    <td>
      <pre>
sp.source
      </pre>
    </td>
  </tr>

  <tr>
    <td>6</td>
    <td>Upgradability</td>
    <td>
      <pre>
      </pre>
      <small>https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable</small>
    </td>
    <td>
      <pre>
      </pre>
      <small>https://smartpy.io/ide?template=upgradable_lambdas.py</small>
      <small>https://tezos.stackexchange.com/questions/3340/what-are-good-examples-of-upgradable-smartpy-contracts-using-proxy-delegates-or</small>
    </td>
  </tr>

  <tr>
    <td>7</td>
    <td>Get Balance Of Token</td>
    <td>
      <pre>
uint256 bal;
bal = IERC20Upgradeable(tokenAddress).balanceOf(targetAddress);
      </pre>
    </td>
    <td>
      <pre>
# solution 1: sp.transfer with delay behaviour 
contract = sp.contract(
    balance_of_param,
    fa2_address,
    "balance_of"
).unwrap_some(error="Fa2BalanceOfNotFound")
param = sp.record(
    callback=sp.self_entrypoint("_setter"),
    requests=requests,
)
sp.transfer(param, sp.tez(0), contract)
# solution 2: call OnchainviewBalanceOf mixin of FA2 contract, no delay
balance = sp.view(
            "get_balance_of",
            fa2_address,
            balance_of_param,
            [balance_of_response],
          ).unwrap_some(error="Invalid view")
      </pre>
      <small>1. https://forum.smartpy.io/t/obtaining-the-user-balance-of-a-deployed-fa2/25/2</small><br/>
      <small>2. <a target="_blank" href="https://smartpy.io/ide?code=eJzdVMtuozAU3fMVFiusifiAjipNiJRdu2l3UYQsMMUS2MjXNMrfzzW@BFySme5GGi_ysM@559yHrfrBWMegF9YNVyaAwZAkv2DIe1OPnUxq2bBeKJ3xpyRhuKpOALCjVVLX@wyBB6OdFZVDAKPlSWWptHJlmYHsmh3rr6@ilyuMX8iuBLgsHO78f3BW6Q8ewzBCXgsn8gBkzxQuucG8Y6OrFp2Wn0peIisBPBn5YsBKN1q9EbhhtikX_33KS8Yv8h8nS262uGbqBSBwljidp_CdAnfCb1HXVgKcY6GodhLTug5GaRflhczQaUosSD1ILBxOyqT4KDNynA8jtETj3@wlUe81U2OR_lCFUOwz_xmRGmMpJlN6azFWuKkE5xjU@8vS0KB0rs@OZXzd33zUFyuGEgxOIef3JjB4Z_Ml@2sZnHGiOz6uBYXtpM42OfHwpmGPSiexTl77OW2UBcf8Rsqnh246o7BUVr9VQiW1sMpk_iUMyUwfYVRxL8erkh5atJxyYv_AE7qtwcR@xs5vZ1rYq9Bsrz_WJAIvImGjiNkFsqVmh9aYLblYO8yXgabQ8ajeQRQLYuXAFwTB8zSSag6tuRAPdqx1fYe4dzv6646zMLxNA@HJR9GBpJDrZoa4UXuj4OuTbyncsk@W8fr68zdw3__F">My code</a></small>
    </td>
  </tr>

   <tr>
    <td>8</td>
    <td>Map</td>
    <td>
      <pre>
# declaration
mapping(address => bool) public my_maps;
# assignment
my_maps[address("0x0000000000000000000000000000000000000000")] = true;
      </pre>
    </td>
    <td>
      <pre>
# declaration
map_type: type = sp.big_map[sp.address, sp.bool]
# assignment
self.data.my_maps = sp.cast(sp.big_map({sp.address("tz1Ke2h7sDdakHJQh8WX4Z372du1KChsksyU"):True}), map_type)
      </pre>
      <small></small>
    </td>
  </tr>
  
  <tr>
    <td>9</td> 
    <td>Enum</td>
    <td>
      <pre>
# declaration
enum status{ PAUSED, PRESALE, SALE }
# assignment
status saleStatus = status.PAUSED;
      </pre>
    </td>
    <td>
      <pre>
# declaration
status:type = sp.variant(paused=sp.unit, presales=sp.unit, sale=sp.unit)        
# assignment
self.data.status = sp.cast(sp.variant.paused(()), status)
      </pre>
      <small></small>
    </td>
  </tr>

   <tr>
    <td>10</td> 
    <td>Internal Function</td>
    <td>
      <pre>
function myInternalFunc(address from, address to, uint256 value) internal {
  ...
}
      </pre>
    </td>
    <td>
      <pre>
@sp.private(with_storage="read-write")
def myInternalFunc(self, from, to, value):
  sp.cast(from, sp.address)
  sp.cast(to, sp.address)
  sp.cast(value, sp.nat)
...
      </pre>
      <small></small>
    </td>
  </tr>

  <tr>
    <td>11</td> 
    <td>Internal View Function</td>
    <td>
      <pre>
function myInternalFunc(uint256 tokenId) internal view returns(uint256) {
  address owner;
  ...
  return owner;
}
      </pre>
    </td>
    <td>
      <pre>
@sp.private(with_storage="read-only")
def myInternalFunc(self, tokenId):
  sp.cast(tokenId, sp.nat)
  owner = ...
  ...
  return sp.cast(owner, sp.address)
      </pre>
      <small></small>
    </td>
  </tr>

  <tr>
    <td>12</td> 
    <td>External View Function</td>
    <td>
      <pre>
function myExternalFunc(uint256 tokenId) external view returns(uint256) {
  address owner;
  ...
  return owner;
}
      </pre>
    </td>
    <td>
      <pre>
@sp.onchain_view
def myExternalFunc(self, tokenId):
  sp.cast(tokenId, sp.nat)
  owner = ...
  ...
  return sp.cast(owner, sp.address)
      </pre>
      <small></small>
    </td>
  </tr>

  <tr>
    <td>13</td> 
    <td>2_Owner.sol</td>
    <td>
      <pre>
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;        
contract Owner {
    address private owner;
    event OwnerSet(address indexed oldOwner, address indexed newOwner);

    modifier isOwner() {
        require(msg.sender == owner, "Caller is not owner");
        _;
    }
    
    constructor() {
        owner = msg.sender; 
        emit OwnerSet(address(0), owner);
    }

    function changeOwner(address newOwner) public isOwner {
        emit OwnerSet(owner, newOwner);
        owner = newOwner;
    }

    function getOwner() external view returns (address) {
        return owner;
    }
}        
      </pre>
    </td>
    <td>
      <pre>
import smartpy as sp

@sp.module
def main():
    OwnerSet:type = sp.record(oldOwner=sp.address, newOwner=sp.address)
    class Owner(sp.Contract):
    
        def __init__(self, owner):
            sp.cast(owner, sp.address)
            self.data.owner = owner
            # cannot emit in constructor 
            # sp.emit(sp.cast(sp.record(oldOwner=sp.address(""), newOwner=owner), OwnerSet), tag="OwnerSet")
            
        @sp.private(with_storage="read-only")
        def isOwner(self, sender):
            assert sender == self.data.owner, "Caller is not owner"
            
        @sp.entrypoint
        def changeOwner(self, newOwner):
            self.isOwner(sp.sender)
            sp.cast(newOwner, sp.address)
            sp.emit(sp.cast(sp.record(oldOwner=self.data.owner, newOwner=newOwner), OwnerSet), tag="OwnerSet")
            self.data.owner = newOwner 
            
        @sp.onchain_view()
        def getOwner(self):
            return self.data.owner
            
@sp.add_test(name="abc")                  
def test():
    admin = sp.test_account("Administrator")
    alice = sp.test_account("Alice")
    s = sp.test_scenario(main) 
    c = main.Owner(admin.address)
    s += c
    s.verify(c.getOwner() == admin.address)
    c.changeOwner(alice.address).run(sender=admin)
      </pre>
      <small></small>
    </td>
  </tr>

  <tr>
    <td>14</td> 
    <td>3_Ballot.sol</td>
    <td>
      <pre>
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Ballot {

    struct Voter {
        uint weight;
        bool voted;
        address delegate;
        uint vote;
    }

    struct Proposal {
        bytes32 name;
        uint voteCount;
    }

    address public chairperson;

    mapping(address => Voter) public voters;

    Proposal[] public proposals;
    constructor(bytes32[] memory proposalNames) {
        chairperson = msg.sender;
        voters[chairperson].weight = 1;

        for (uint i = 0; i < proposalNames.length; i++) {
            proposals.push(Proposal({
                name: proposalNames[i],
                voteCount: 0
            }));
        }
    }

    function giveRightToVote(address voter) public {
        require(
            msg.sender == chairperson,
            "Only chairperson can give right to vote."
        );
        require(
            !voters[voter].voted,
            "The voter already voted."
        );
        require(voters[voter].weight == 0);
        voters[voter].weight = 1;
    }

    function delegate(address to) public {
        Voter storage sender = voters[msg.sender];
        require(!sender.voted, "You already voted.");
        require(to != msg.sender, "Self-delegation is disallowed.");

        while (voters[to].delegate != address(0)) {
            to = voters[to].delegate;
            require(to != msg.sender, "Found loop in delegation.");
        }
        sender.voted = true;
        sender.delegate = to;
        Voter storage delegate_ = voters[to];
        if (delegate_.voted) {
            proposals[delegate_.vote].voteCount += sender.weight;
        } else {
            delegate_.weight += sender.weight;
        }
    }

    function vote(uint proposal) public {
        Voter storage sender = voters[msg.sender];
        require(sender.weight != 0, "Has no right to vote");
        require(!sender.voted, "Already voted.");
        sender.voted = true;
        sender.vote = proposal;

        proposals[proposal].voteCount += sender.weight;
    }

    function winningProposal() public view
            returns (uint winningProposal_)
    {
        uint winningVoteCount = 0;
        for (uint p = 0; p < proposals.length; p++) {
            if (proposals[p].voteCount > winningVoteCount) {
                winningVoteCount = proposals[p].voteCount;
                winningProposal_ = p;
            }
        }
    }

    function winnerName() public view
            returns (bytes32 winnerName_)
    {
        winnerName_ = proposals[winningProposal()].name;
    }
}        
      </pre>
    </td>
    <td>
      <pre>
      </pre>
      <small></small>
    </td>
  </tr>

  <tr>
    <td>15</td> 
    <td></td>
    <td>
      <pre>
      </pre>
    </td>
    <td>
      <pre>
      </pre>
      <small></small>
    </td>
  </tr>

  <tr>
    <td>16</td> 
    <td></td>
    <td>
      <pre>
      </pre>
    </td>
    <td>
      <pre>
      </pre>
      <small></small>
    </td>
  </tr>

  <tr>
    <td>17</td> 
    <td></td>
    <td>
      <pre>
      </pre>
    </td>
    <td>
      <pre>
      </pre>
      <small></small>
    </td>
  </tr>
</table>
