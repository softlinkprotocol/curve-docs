.. _guide-curve:

=====
Curve
=====

Implementing a Curve Pool
=========================

Creating a new Curve Pool requires some familiarity with the following tools:

- `eth-brownie <https://eth-brownie.readthedocs.io/en/stable/>`_
- `ganache-cli <https://github.com/trufflesuite/ganache-cli>`_
- `pytest <https://docs.pytest.org/en/stable/>`_
- `vyper <https://vyper.readthedocs.io/en/stable/>`_

You should also have API keys from both `Infura <https://infura.io/>`_ and `Etherscan <https://etherscan.io/apis>`_, and set the following environment variables:

- ``WEB3_INFURA_PROJECT_ID``
- ``ETHERSCAN_TOKEN``

Preparation
-----------

Before creating a new pool, some research is required to check the behavior of the component tokens' contracts. Below is a short and non-exhaustive list of things to check for during your research.

> The key thing in this phase is to verify **which** behavior happens, so that the pool can be modified to handle the behavior correctly

- [ ] Check `EIP-20 <https://eips.ethereum.org/EIPS/eip-20>`_ token functions ``approve``, ``transfer``, and ``transferFrom``

  > The EIP-20 specification does not dictate how a contract should behave during a successful or failing transfer. Returning ``True`` and reverting is the most common response, but other possible behaviors include returning ``None`` / reverting or returning ``True`` / returning ``False``

  - What are the return values for a successful call?

  - Does the contract revert if these calls are unsuccessful?
  - Are there any side-effects from a successful/unsuccessful call?

  - Check for, and take note of, unexpected approval behavior
    - ``approve`` reverts when approving an amount greater than an account's balance
    - ``approve`` reverts when doing a non-zero to non-zero approval

- [ ] Check for transfer fees or the potential to introduce a transfer fee in the future

- `USDT <https://etherscan.io/address/0xdac17f958d2ee523a2206206994597c13d831ec7>`_ is an asset which, has the capability to charge a transfer fee, *but does not currently do so*

- [ ] Verify that each token address and respective contract source code is correct

> By all means this is not an exhaustive list and more items may be added in the future to check for prior to pool creation. Main priority is to always do a sniff test and double check to verify functionality.

Implementation
--------------

This portion of the guide requires you have the `curvefi/curve-contract <https://github.com/curvefi/curve-contract>`_ repository forked, cloned locally (of course) and have already setup a virtual environment for it.

> Remember to commit often, and follow the `Conventional Commit Standard <https://www.conventionalcommits.org/en/v1.0.0/>`_

1. Create a new branch (convention is to prefix ``pool_`` to the branch name)
2. Create a sub-directory in the `contracts/pools/ <https://github.com/curvefi/curve-contract/tree/master/contracts/pools>`_ directory named after the pool you'll be creating
3. Typically you'll start a new pool by copying the appropriate templates from the `contracts/pool-templates/ <https://github.com/curvefi/curve-contract/tree/master/contracts/pool-templates>`_ directory
   - Read through the `README <https://github.com/curvefi/curve-contract/blob/master/contracts/pool-templates/README.md>`_ in the ``pool-templates`` directory for more information on which template to use and additional steps needed to correctly configure the template.
   - Take a moment to read through the template to verify it's correctness (and also to check your understanding)

4. Create/Adapt a `pooldata.json <https://github.com/curvefi/curve-contract/tree/master/contracts/pools#adding-a-new-pool>`_ file for your new pool
   - Prior to actual ``mainnet`` deployment, you will be missing certain fields, for example ``gauge_addresses``, ``lp_token_address``, and others
   - Make sure to double/triple check the addresses for accuracy
5. Include a ``README.md`` for your pool using the same format as the other pools.
   - You can adapt a ``README.md`` from another pool

Testing
-------

> Code is law on-chain, and there are no reverting commits once you deploy to ``mainnet``

Testing is important, even more important when once your code gets deployed it becomes immutable. This is by far the most fun section of this guide and, and it will easily consume the most of your time.

1. Verify the ``curve-contract`` test suite passes for your newly implemented pool

   - ``brownie test --pool [name]``, where ``name`` is the pool subdirectory name

   - Run the ``tests/forked`` tests on your local ``mainnet-fork``, ``brownie tests tests/forked/ --network mainnet-fork --pool [name]``
     - These tests use the actual pool tokens in a forked ``mainnet`` and serves as a final check for any irregularities within the actual token

2. Add a CI work flow file to `.github/workflows <https://github.com/curvefi/curve-contract/tree/master/.github/workflows>`_ for your pool, which you can adapt from any of the existing work flows

   - Use search and replace to appropriately adapt the work flow for your pool

Fee Burn Verification
*********************

> This portion of testing may be a little more involved, be warned

It's important that we verify the process of collecting and burning fees for the new pool. For many cases, one of the `existing burners <https://github.com/curvefi/curve-dao-contracts/tree/master/contracts/burners>`_ will already be able to handle fees for your pool. Select the correct burner, add your pool token(s) to the appropriate `burner test <https://github.com/curvefi/curve-dao-contracts/tree/master/tests/fork/Burners>`_, and run it in a forked ``mainnet`` to verify.

8. Clone the `curvefi/curve-dao-contracts <https://github.com/curvefi/curve-dao-contracts/>`_ repository and ``cd`` into it

2. For many cases, one of the `existing burners <https://github.com/curvefi/curve-dao-contracts/tree/master/contracts/burners>`_ will already be able to handle fees for your pool. Select the correct burner, add your pool token(s) to the appropriate `burner test <https://github.com/curvefi/curve-dao-contracts/tree/master/tests/fork/Burners>`_, and run it in a forked `mainnet` to verify.

   > Note: Short of a full end-to-end verification, the pool tests in ``curve-contract/tests/pools/common/unitary/test_claim_fees.py`` verify the process works correctly

   - If a new burner is required, speak to @iamdefinitelyahuman

Special Requirements
--------------------

In this step you'll need to verify and handle any special requirements for pool incentives.

- Some teams will want to incentivize pools with additional rewards. In most cases this is handled through a vanilla `SNX rewards contract <https://github.com/iamdefinitelyahuman/unipool-fork>`_. Depending on the team you may or may not have to help them deploy and configure this contract.
- In some cases reward tokens can only be sent straight into the pool (such as with ``COMP``). This will require special logic built into the pool, and must be handled on a case-by-case basis.

Deployment and Configuration
----------------------------

1. Run the `deployment script <https://github.com/curvefi/curve-contract/blob/master/scripts/deploy.py>`_ to deploy the pool and gauge.

   - Set the ``DEPLOYER`` constant to load from a key store, or use a throwaway private key.

   - Set the ``POOL_NAME`` constant with the name of the subdirectory that the pool you are deploying is located in.

   - If the pool is expected to receive incentives, modify ``GAUGE_OWNER`` to retain ownership via an EOA so the rewards may be configured.

   - You may also wish to modify ``POOL_OWNER`` and ``GAUGE_OWNER`` to retain ownership of the contracts in case they need to be killed quickly.

   - Verify the deployment process in a forked ``mainnet``, ``brownie run deploy --network mainnet-fork``

2. Deploy the pool on ``mainnet``

   - ``brownie run deploy --network mainnet``

3. Add the pool to the registry using `scripts in the registy repo <https://github.com/curvefi/curve-pool-registry/tree/master/scripts/>`_:

   - Verify that all deployment addresses are correct within the ``pooldata.json`` file for the pool, and that the pool has been merged to the master branch of the main repository. This is required to update the registry.

   - Within the registry repository, run the following script to fetch the pool data locally, ``brownie run get_pool_data``

   - In `add_pools.py <https://github.com/curvefi/curve-pool-registry/tree/master/scripts/add_pools.py>`_, set the `DEPLOYER` constant to load an account with authority to modify the registry.

   - Add the pool with the following script, ``brownie run add_pools --network mainnet``

4. Deploy and/or configure burner contracts as needed.

5. Work with other teams to deploy and configure any required rewards contract, and configure the gauge to work with the reward contract.

6. `Create a DAO vote <https://github.com/curvefi/curve-dao-contracts/blob/master/scripts/voting/new_vote.py>`_ to add the new gauge (and fee burner, if required).

Congratulations
---------------

You've made it to the end, all your hard work has paid off!
