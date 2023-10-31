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
# solution 2: call FA2 contract with OnchainviewBalanceOf mixin, no delay
contract = sp.contract(
                balance_of_param,
                fa2_address,
                "get_balance_of"
            ).unwrap_some(error="Fa2GetBalanceOfNotFound")
      </pre>
      <small>https://forum.smartpy.io/t/obtaining-the-user-balance-of-a-deployed-fa2/25/2</small>
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
self.data.my_maps = sp.big_map({sp.address("tz1Ke2h7sDdakHJQh8WX4Z372du1KChsksyU"):True})
sp.cast(self.data.my_maps, map_type)
      </pre>
      <small></small>
    </td>
  </tr>
  
  <tr>
    <td>9</td> 
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
    <td>10</td> 
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
    <td>11</td> 
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
    <td>12</td> 
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
    <td>13</td> 
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
