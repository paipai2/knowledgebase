<table>
  <tr><th>Description</th><th>Solidity</th><th>Tezos</th></tr>
  <tr>
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
    <td>msg.sender</td>
    <td>
      <pre>
msg.sender
      </pre>
    </td>
    <td>
      <pre>
sp.source
      </pre>
    </td>
  </tr>

  <tr>
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
