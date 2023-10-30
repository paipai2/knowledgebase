<table>
  <tr><th>Description</th><th>Solidity</th><th>Tezos</th></tr>
  <tr>
    <td>Blackhole Address</td>
    <td>0x0000000000000000000000000000000000000000</td>
    <td>
      tz1Ke2h7sDdakHJQh8WX4Z372du1KChsksyU<br/>
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
# https://smartpy.io/manual/scenarios/testing_contracts#calls-optional-arguments        
scenario += c1.ep().run(now = sp.timestamp(100))
      </pre>
    </td>
  </tr>
</table>
