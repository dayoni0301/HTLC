# HTLC

 HTLC lock 소스코드를 활용하여 ethereum testnet의 ethereum wallet 계정에서 스마트 컨트랙트로 동작시키고,
이를 Web3.js 로 연계 호출하여 동작하는 애플리케이션 개발.

스마트 컨트렉트: 특정 계약을 스스로수립, 검증, 이행하기위한 컴퓨터 프로토콜

<Answer.sol>

pragma solidity ^0.8.21;contract Answer {
 uint answer;function setAnswer(uint _answer) public {
  answer = _answer;
 }function getAnswer() 
 view public returns (uint) {
  return answer;
 }
}

<deploy.js>

module.exports = function(_deployer) {
  // Use deployer to state migration tasks.
  var Answer = artifacts.require("Answer");module.exports = function(deployer) {
    deployer.deploy(Answer);
   };
};

<test.js>

pragma solidity ^0.8.21;import "truffle/Assert.sol";
import "truffle/DeployedAddresses.sol";
import "../contracts/Answer.sol";contract TestAnswer {
 function testAnswer() public {
  Answer a = new Answer();  uint _expected = 42;
  a.setAnswer(_expected);  Assert.equal(a.getAnswer(), _expected, "The Answer is 42.");
 }
}
