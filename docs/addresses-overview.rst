.. _addresses-overview:

=========
Addresses
=========

Here is a list of all current contract deployments within the Curve protocol.

Mainnet Contracts
=================

Base Pools
----------

For each base pool there exist multiple deployed contracts:

- ``StableSwap<pool>.vy``: Curve stablecoin AMM contract
- ``Deposit<pool>.vy``: contract used to wrap underlying tokens prior to depositing them into the pool
- ``CurveContract<version>.vy``: LP token contract for the pool


.. csv-table::
   :header: "Pool", "Source", "Address"

   Compound, `StableSwapCompound.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/pools/compound/StableSwapCompound.vy>`_, `0xA2B47E3D5c44877cca798226B7B8118F9BFb7A56 <https://etherscan.io/address/0xA2B47E3D5c44877cca798226B7B8118F9BFb7A56#code>`_
   Compound, `DepositCompound.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/pools/compound/DepositCompound.vy>`_, `0xeb21209ae4c2c9ff2a86aca31e123764a3b6bc06 <https://etherscan.io/address/0xeb21209ae4c2c9ff2a86aca31e123764a3b6bc06#code>`_
   Compound, `CurveContractV1.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/tokens/CurveTokenV1.vy>`_, `0x845838DF265Dcd2c412A1Dc9e959c7d08537f8a2 <https://etherscan.io/address/0x845838DF265Dcd2c412A1Dc9e959c7d08537f8a2#code>`_



Meta Pools
----------

.. csv-table:: 
   :header: "Pool", "Source", "Address"

   GUSD, `StableSwapGUSD.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/pools/gusd/StableSwapGUSD.vy>`_, `0x4f062658EaAF2C1ccf8C8e36D6824CDf41167956 <https://etherscan.io/address/0x4f062658EaAF2C1ccf8C8e36D6824CDf41167956>`_


Burners
-------
.. csv-table::
   :header: "Gauge", "Source", "Address"

   ABurner, `ABurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/ABurner.vy>`_, `0xAbADFd391b3821f3C80D48a59229769D0b677d2E <https://etherscan.io/address/0xAbADFd391b3821f3C80D48a59229769D0b677d2E#code>`_
   BTCBurner, `BTCBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/BTCBurner.vy>`_, `0x00702BbDEaD24C40647f235F15971dB0867F6bdB <https://etherscan.io/address/0x00702BbDEaD24C40647f235F15971dB0867F6bdB#code>`_
   CBurner, `CBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/CBurner.vy>`_, `0x55858AdaBb9EA24dDd0678DB0E9b41D8bD48e7EE <https://etherscan.io/address/0x55858AdaBb9EA24dDd0678DB0E9b41D8bD48e7EE#code>`_
   ETHBurner, `ETHBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/ETHBurner.vy>`_, `0xD782EbD4bAbd95c2D8255112eFc6DD865c849394 <https://etherscan.io/address/0xD782EbD4bAbd95c2D8255112eFc6DD865c849394#code>`_
   EuroBurner, `EuroBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/EuroBurner.vy>`_, `0x3a16b6001201577CC67bDD8aAE5A105bbB035882 <https://etherscan.io/address/0x3a16b6001201577CC67bDD8aAE5A105bbB035882#code>`_
   IdleBurner, `IdleBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/IdleBurner.vy>`_, `0xd1EBEf836f25047bB6AaC2DCD8618Efe2DC17D67 <https://etherscan.io/address/0xd1EBEf836f25047bB6AaC2DCD8618Efe2DC17D67#code>`_
   LPBurner, `LPBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/LPBurner.vy>`_, `0xaa42C0CD9645A58dfeB699cCAeFBD30f19B1ff81 <https://etherscan.io/address/0xaa42C0CD9645A58dfeB699cCAeFBD30f19B1ff81#code>`_
   MetaBurner, `MetaBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/MetaBurner.vy>`_, `0xE4b65889469ad896e866331f0AB5652C1EcfB3E6 <https://etherscan.io/address/0xE4b65889469ad896e866331f0AB5652C1EcfB3E6#code>`_
   USDNBurner, `USDNBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/USDNBurner.vy>`_, `0x06534b0BF7Ff378F162d4F348390BDA53b15fA35 <https://etherscan.io/address/0x06534b0BF7Ff378F162d4F348390BDA53b15fA35#code>`_
   UnderlyingBurner, `UnderlyingBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/UnderlyingBurner.vy>`_, `0x874210cF3dC563B98c137927e7C951491A2e9AF3 <https://etherscan.io/address/0x874210cF3dC563B98c137927e7C951491A2e9AF3#code>`_
   YBurner, `YBurner.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/burners/YBurner.vy>`_, `0x94c866a48EF49Db7Bf24207F2752E69BA85F6287 <https://etherscan.io/address/0x94c866a48EF49Db7Bf24207F2752E69BA85F6287#code>`_


Liquidity Gauges
----------------
.. csv-table::
   :header: "Gauge", "Source", "Address"
   
   3pool, `LiquidityGauge.sol <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0xbFcF63294aD7105dEa65aA58F8AE5BE2D9d0952A <https://etherscan.io/address/0xbFcF63294aD7105dEa65aA58F8AE5BE2D9d0952A#code>`_,
   aave, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0xd662908ADA2Ea1916B3318327A97eB18aD588b5d <https://etherscan.io/address/0xd662908ADA2Ea1916B3318327A97eB18aD588b5d#code>`_,
   bbtc, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0xdFc7AdFa664b08767b735dE28f9E84cd30492aeE <https://etherscan.io/address/0xdFc7AdFa664b08767b735dE28f9E84cd30492aeE#code>`_,
   bUSD, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0x69Fb7c45726cfE2baDeE8317005d3F94bE838840 <https://etherscan.io/address/0x69Fb7c45726cfE2baDeE8317005d3F94bE838840#code>`_,
   Compound, `LiquidityGauge.sol <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0x7ca5b0a2910B33e9759DC7dDB0413949071D7575 <https://etherscan.io/address/0x7ca5b0a2910B33e9759DC7dDB0413949071D7575#code>`_,
   dusd, `LiquidityGaugeReward.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGaugeReward.vy>`_, `0xAEA6c312f4b3E04D752946d329693F7293bC2e6D <https://etherscan.io/address/0xAEA6c312f4b3E04D752946d329693F7293bC2e6D#code>`_,
   eurs, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0x90Bb609649E0451E5aD952683D64BD2d1f245840 <https://etherscan.io/address/0x90Bb609649E0451E5aD952683D64BD2d1f245840#code>`_,
   gusd, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0xC5cfaDA84E902aD92DD40194f0883ad49639b023 <https://etherscan.io/address/0xC5cfaDA84E902aD92DD40194f0883ad49639b023#code>`_,
   hbtc, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0x4c18E409Dc8619bFb6a1cB56D114C3f592E0aE79 <https://etherscan.io/address/0x4c18E409Dc8619bFb6a1cB56D114C3f592E0aE79#code>`_,
   husd, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0x2db0E83599a91b508Ac268a6197b8B14F5e72840 <https://etherscan.io/address/0x2db0E83599a91b508Ac268a6197b8B14F5e72840#code>`_,
   musd, `LiquidityGaugeReward.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGaugeReward.vy>`_, `0x5f626c30EC1215f4EdCc9982265E8b1F411D1352 <https://etherscan.io/address/0x5f626c30EC1215f4EdCc9982265E8b1F411D1352#code>`_,
   obtc, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0x11137B10C210b579405c21A07489e28F3c040AB1 <https://etherscan.io/address/0x11137B10C210b579405c21A07489e28F3c040AB1#code>`_,
   PAX, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0x64E3C23bfc40722d3B649844055F1D51c1ac041d <https://etherscan.io/address/0x64E3C23bfc40722d3B649844055F1D51c1ac041d#code>`_,
   pbtc, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0xd7d147c6Bb90A718c3De8C0568F9B560C79fa416 <https://etherscan.io/address/0xd7d147c6Bb90A718c3De8C0568F9B560C79fa416#code>`_,
   renBTC, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0xB1F2cdeC61db658F091671F5f199635aEF202CAC <https://etherscan.io/address/0xB1F2cdeC61db658F091671F5f199635aEF202CAC#code>`_,
   rsv, `LiquidityGaugeReward.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGaugeReward.vy>`_, `0x4dC4A289a8E33600D8bD4cf5F6313E43a37adec7 <https://etherscan.io/address/0x4dC4A289a8E33600D8bD4cf5F6313E43a37adec7#code>`_,
   sbtc, `LiquidityGaugeReward.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGaugeReward.vy>`_, `0x705350c4BcD35c9441419DdD5d2f097d7a55410F <https://etherscan.io/address/0x705350c4BcD35c9441419DdD5d2f097d7a55410F#code>`_,
   seth, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0x3C0FFFF15EA30C35d7A85B85c0782D6c94e1d238 <https://etherscan.io/address/0x3C0FFFF15EA30C35d7A85B85c0782D6c94e1d238#code>`_,
   steth, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0x182B723a58739a9c974cFDB385ceaDb237453c28 <https://etherscan.io/address/0x182B723a58739a9c974cFDB385ceaDb237453c28#code>`_,
   susdv2, `LiquidityGaugeReward.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGaugeReward.vy>`_, `0xA90996896660DEcC6E997655E065b23788857849 <https://etherscan.io/address/0xA90996896660DEcC6E997655E065b23788857849#code>`_,
   tbtc, `LiquidityGaugeReward.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGaugeReward.vy>`_, `0x6828bcF74279eE32f2723eC536c22c51Eed383C6 <https://etherscan.io/address/0x6828bcF74279eE32f2723eC536c22c51Eed383C6#code>`_,
   usdk, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0xC2b1DF84112619D190193E48148000e3990Bf627 <https://etherscan.io/address/0xC2b1DF84112619D190193E48148000e3990Bf627#code>`_,
   usdn, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0xF98450B5602fa59CC66e1379DFfB6FDDc724CfC4 <https://etherscan.io/address/0xF98450B5602fa59CC66e1379DFfB6FDDc724CfC4#code>`_,
   USDT, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0xBC89cd85491d81C6AD2954E6d0362Ee29fCa8F53 <https://etherscan.io/address/0xBC89cd85491d81C6AD2954E6d0362Ee29fCa8F53#code>`_,
   ust, `LiquidityGaugeV2.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/gauges/LiquidityGaugeV2.vy>`_, `0x3B7020743Bc2A4ca9EaF9D0722d42E20d6935855 <https://etherscan.io/address/0x3B7020743Bc2A4ca9EaF9D0722d42E20d6935855#code>`_,
   Y, `LiquidityGauge.vy <https://github.com/curvefi/curve-contract/blob/master/contracts/gauges/LiquidityGauge.vy>`_, `0xFA712EE4788C042e2B7BB55E6cb8ec569C4530c1 <https://etherscan.io/address/0xFA712EE4788C042e2B7BB55E6cb8ec569C4530c1#code>`_,


Pool Registry
-------------

.. csv-table::
   :header: "Name", "Source", "Address"

   Address Provider, `AddressProvider.vy <https://github.com/curvefi/curve-pool-registry/blob/master/contracts/AddressProvider.vy>`_, `0x0000000022d53366457f9d5e68ec105046fc4383 <https://etherscan.io/address/0x0000000022d53366457f9d5e68ec105046fc4383#code>`_
   Curve Calculator, `CurveCalc.vy <https://github.com/curvefi/curve-pool-registry/blob/master/contracts/CurveCalc.vy>`_, `0xc1DB00a8E5Ef7bfa476395cdbcc98235477cDE4E <https://etherscan.io/address/0xc1DB00a8E5Ef7bfa476395cdbcc98235477cDE4E#code>`_
   Pool Info, `PoolInfo.vy <https://github.com/curvefi/curve-pool-registry/blob/master/contracts/PoolInfo.vy>`_, `0xe64608E223433E8a03a1DaaeFD8Cb638C14B552C <https://etherscan.io/address/0xe64608E223433E8a03a1DaaeFD8Cb638C14B552C#code>`_
   Registry, `Registry.vy <https://github.com/curvefi/curve-pool-registry/blob/master/contracts/Registry.vy>`_, `0x7D86446dDb609eD0F5f8684AcF30380a356b2B4c <https://etherscan.io/address/0x7D86446dDb609eD0F5f8684AcF30380a356b2B4c#code>`_





Curve DAO
---------

.. csv-table::
   :header: "Name", "Source", "Address"

   CRV Token, `ERC20CRV.sol <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/ERC20CRV.vy>`_, `0xD533a949740bb3306d119CC777fa900bA034cd52 <https://etherscan.io/address/0xD533a949740bb3306d119CC777fa900bA034cd52#code>`_
   Fee Distributor, `FeeDistributor.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/FeeDistributor.vy>`_, `0xA464e6DCda8AC41e03616F95f4BC98a13b8922Dc <https://etherscan.io/address/0xA464e6DCda8AC41e03616F95f4BC98a13b8922Dc#code>`_
   Gauge Controller, `GaugeController.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/GaugeController.vy>`_, `0x2F50D538606Fa9EDD2B11E2446BEb18C9D5846bB <https://etherscan.io/address/0x2F50D538606Fa9EDD2B11E2446BEb18C9D5846bB#code>`_
   Gauge Proxy, `GaugeProxy.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/GaugeProxy.vy>`_, `0x519AFB566c05E00cfB9af73496D00217A630e4D5 <https://etherscan.io/address/0x519AFB566c05E00cfB9af73496D00217A630e4D5#code>`_
   Minter, `Minter.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/Minter.vy>`_, `0xd061D61a4d941c39E5453435B6345Dc261C2fcE0 <https://etherscan.io/address/0xd061D61a4d941c39E5453435B6345Dc261C2fcE0#code>`_
   Pool Proxy, `PoolProxy.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/PoolProxy.vy>`_, `0x6e8f6D1DA6232d5E40b0B8758A0145D6C5123eB7 <https://etherscan.io/address/0x6e8f6D1DA6232d5E40b0B8758A0145D6C5123eB7#code>`_
   Voting Escrow, `VotingEscrow.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/VotingEscrow.vy>`_, `0x5f3b5DfEb7B28CDbD7FAba78963EE202a494e2A2 <https://etherscan.io/address/0x5f3b5DfEb7B28CDbD7FAba78963EE202a494e2A2#code>`_
   Vesting Escrow, `VestingEscrow.vy <https://github.com/curvefi/curve-dao-contracts/blob/master/contracts/VestingEscrow.vy>`_, `0x575ccd8e2d300e2377b43478339e364000318e2c <https://etherscan.io/address/0x575ccd8e2d300e2377b43478339e364000318e2c#code>`_
