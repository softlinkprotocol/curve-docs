.. _exchange-pools:

=======================
Curve StableSwap: Pools
=======================

A Curve pool is a smart contract that implements the StableSwap invariant and thereby allows for the exchange of two tokens.

More broadly, Curve pools can be split into three categories:

* ``Plain pools``
* ``Lending pools``
* ``Metapools``

Source code for Curve pools may be viewed on `GitHub <https://github.com/curvefi/curve-contract/tree/master/contracts>`_.

.. warning::
    The API for plain, lending and metapools applies to all pools that are implemented based on `pool templates <https://github.com/curvefi/curve-contract/tree/master/contracts/pool-templates>`_. When interacting with older Curve pools, there may be differences in terms of visibility, gas efficiency and/or variable naming. Please **do not** assume for a Curve pool to implement the API outlined in this section and verify this.

For any code style information, please refer to the official :ref:`style guide <guide-code-style>`.


Plain Pools
===========

The simplest Curve pool is a plain pool, which is an implementation of the StableSwap invariant for two or more tokens. The key characteristic of a plain pool is that the pool contract holds **all** deposited assets at all times.

An example of a Curve plain pool is `3Pool <https://github.com/curvefi/curve-contract/tree/master/contracts/pools/3pool>`_, which contains the tokens ``DAI``, ``USDC`` and ``USDT``.

.. note::
    The API of plain pools is also implemented by lending and metapools.

The Brownie console interaction examples are using `EURS Pool <https://etherscan.io/address/0x0Ce6a5fF5217e38315f87032CF90686C96627CAA>`_.

Getting Pool Info
-----------------

.. py:function:: StableSwap.coins(i: uint256) -> uint256: view

    Getter for the array of swappable coins within the pool. The last coin will always be the LP token of the base pool.

    .. code-block:: python

        >>> pool.coins(0)
        '0xdB25f211AB05b1c97D595516F45794528a807ad8'

.. py:function:: StableSwap.balances(i: uint256) -> uint256: view

    Getter for the pool balances array.

    .. code-block:: python

        >>> pool.balances(0)
        2918187395

.. py:function:: StableSwap.owner() -> uint256: view

    Getter for the admin/owner of the pool.

    .. code-block:: python

        >>> pool.owner()
        '0xeCb456EA5365865EbAb8a2661B0c503410e9B347'

.. py:function:: StableSwap.lp_token() -> uint256: view

    Getter for the :ref:`LP token <exchange-lp-tokens>` of the pool.

    .. code-block:: python

        >>> pool.lp_token()
        '0x194eBd173F6cDacE046C53eACcE9B953F28411d1'


.. py:function:: StableSwap.A() -> uint256: view

    The :ref:`amplification coefficient <exchange-pools-A>` for the pool.

    .. code-block:: python

        >>> pool.A()
        100

.. py:function:: StableSwap.A_precise() -> uint256: view

    The :ref:`amplification coefficient <exchange-pools-A>` for the pool not scaled by ``A_PRECISION`` (``100``).

    .. code-block:: python

        >>> pool.A_precise()
        10000

.. py:function:: StableSwap.get_virtual_price() -> uint256: view

    The current price of the pool LP token relative to the underlying pool assets. Given as an integer with 1e18 precision.

    .. code-block:: python

        >>> pool.get_virtual_price()
        1001692838188850782

.. py:function:: StableSwap.fee() -> uint256: view

    The pool swap fee, as an integer with 1e10 precision.

    .. code-block:: python

        >>> pool.fee()
        4000000

.. py:function:: StableSwap.admin_fee() -> uint256: view

    The percentage of the swap fee that is taken as an admin fee, as an integer with with 1e10 precision.

    For factory pools this is hardcoded at 50% (``5000000000``).

    .. code-block:: python

        >>> pool.admin_fee()
        5000000000

.. py:function:: StableSwap.calc_token_amount(_amounts: uint256[N_COINS], _is_deposit: bool) -> uint256: view

    Calculate addition or reduction in token supply from a deposit or withdrawal.

    * ``_amounts``: Amount of each coin being deposited
    * ``_is_deposit``: Set True for deposits, False for withdrawals

    Returns the expected amount of LP tokens received. This calculation accounts for slippage, but not fees.

    .. code-block:: python

        >>> pool.calc_token_amount([10**2, 10**18], True)
        1996887509167925969

Making Exchanges
----------------

.. py:function:: StableSwap.get_dy(i: int128, j: int128, _dx: uint256) -> uint256: view

    Get the amount of coin ``j`` one would receive for swapping ``_dx`` of coin ``i``.

    .. code-block:: python

        >>> pool.get_dy(0, 1, 100)
        996307731416690125

    *Note*: In the ``EURS Pool``, the decimals for ``coins(0)`` and ``coins(1)`` are 2 and 18, respectively.

.. py:function:: StableSwap.exchange(i: int128, j: int128, _dx: uint256, _min_dy: uint256) -> uint256

    Perform an exchange between two coins.

    * ``i``: Index value for the coin to send
    * ``j``: Index value of the coin to receive
    * ``_dx``: Amount of ``i`` being exchanged
    * ``_min_dy``: Minimum amount of ``j`` to receive

    Returns the actual amount of coin ``j`` received. Index values can be found via the ``coins`` public getter method.

    .. code-block:: python

        >>> expected = pool.get_dy(0, 1, 10**2) * 0.99
        >>> pool.exchange(0, 1, 10**2, expected, {"from": alice})


Adding/Removing Liquidity
-------------------------

.. py:function:: StableSwap.add_liquidity(_amounts: uint256[N_COINS], _min_mint_amount: uint256) -> uint256

    Deposit coins into the pool.

    * ``_amounts``: List of amounts of coins to deposit
    * ``_min_mint_amount``: Minimum amount of LP tokens to mint from the deposit

    Returns the amount of LP tokens received in exchange for the deposited tokens.


.. py:function:: StableSwap.remove_liquidity(_amount: uint256, _min_amounts: uint256[N_COINS]) -> uint256[N_COINS]

    Withdraw coins from the pool.

    * ``_amount``: Quantity of LP tokens to burn in the withdrawal
    * ``_min_amounts``: Minimum amounts of underlying coins to receive

    Returns a list of the amounts for each coin that was withdrawn.

.. py:function:: StableSwap.remove_liquidity_imbalance(_amounts: uint256[N_COINS], _max_burn_amount: uint256) -> uint256

    Withdraw coins from the pool in an imbalanced amount.

    * ``_amounts``: List of amounts of underlying coins to withdraw
    * ``_max_burn_amount``: Maximum amount of LP token to burn in the withdrawal

    Returns actual amount of the LP tokens burned in the withdrawal.

.. py:function:: StableSwap.calc_withdraw_one_coin(_token_amount: uint256, i: int128) -> uint256

    Calculate the amount received when withdrawing a single coin.

    * ``_token_amount``: Amount of LP tokens to burn in the withdrawal
    * ``i``: Index value of the coin to withdraw

.. py:function:: StableSwap.remove_liquidity_one_coin(_token_amount: uint256, i: int128, _min_amount: uint256) -> uint256

    Withdraw a single coin from the pool.

    * ``_token_amount``: Amount of LP tokens to burn in the withdrawal
    * ``i``: Index value of the coin to withdraw
    * ``_min_amount``: Minimum amount of coin to receive

    Returns the amount of coin ``i`` received.


Lending Pools
=============

Curve pools may contain lending functionality, whereby the underlying tokens are lent out on other protocols (e.g., Compound or Yearn). Hence, the main difference to a plain pool is that a lending pool does **not** hold the underlying token itself, but rather a **wrapped** representation of it. By allocating liquidity to other protocols, liquidity providers to the Curve pool can receive interest in addition to trading fees.

An example of a Curve lending pool is `Compound Pool <https://github.com/curvefi/curve-contract/tree/master/contracts/pools/compound>`_, which contains the wrapped tokens ``cDAI`` and ``cUSDC``, while the underlying tokens ``DAI`` and ``USDC`` are lent out on Compound. Liquidity providers of the Compound Pool therefore receive interest generated on Compound in addition to fees from token swaps in the pool.

Implementation of lending pools may differ with respect to how wrapped tokens accrue interest. There are two main types of wrapped tokens that are used by lending pools:

    * ``cToken-style tokens``: These are tokens, such as interest-bearing cTokens on Compound (e.g., ``cDAI``), where interest accrues as the rate of the token increases.
    * ``aToken-style tokens``: These are tokens, such as aTokens on AAVE (e.g., ``aDAI``), where interest accrues as the balance of the token increases.


Making Exchanges
----------------

.. py:function:: StableSwap.exchange_underlying(i: int128, j: int128, dx: uint256, min_dy: uint256)

    Perform an exchange between two **underlying** tokens. Index values can be found via the ``underlying_coins`` public getter method.




Metapools
=========



Admin Pool Settings
===================

The following are methods that may only be called by the pool admin (``owner``).

Additionally, some admin methods require a two-phase transaction process, whereby changes are committed in a first transaction and after a forced delay applied via a second transaction. The minimum delay after which a committed action can be applied is given by the constant pool attribute ``admin_actions_delay``, which is set to 3 days.

Pool Ownership
--------------

.. py:function:: StableSwap.commit_transfer_ownership(_owner: address)

    Initiate an ownership transfer of pool to ``_owner``.

    Callable only by the ownership admin. The ownership can not be transferred before ``transfer_ownership_deadline``, which is the timestamp of the current block delayed by ``admin_actions_delay``.

.. py:function:: StableSwap.apply_transfer_ownership()

    Transfers ownership of the pool from current owner to the owner previously set via ``commit_transfer_ownership``.

    .. warning::
        Pool ownership can only be transferred once.


.. py:function:: StableSwap.revert_transfer_ownership()

    Reverts any previously committed transfer of ownership. This method resets the ``transfer_ownership_deadline`` to ``0``.

.. _exchange-pools-A:

Amplification Coefficient
-------------------------

The amplification co-efficient (“A”) determines a pool’s tolerance for imbalance between the assets within it. A higher value means that trades will incure slippage sooner as the assets within the pool become imbalanced.

The appropriate value for A is dependent upon the type of coin being used within the pool.

It is possible to modify the amplification coefficient for a pool after it has been deployed. However, it requires a vote within the Curve DAO and must reach a 15% quorum.

.. py:function:: StableSwap.ramp_A(_future_A: uint256, _future_time: uint256)

    Ramp ``A`` up or down by setting a new ``A`` to take effect at a future point in time.

    * ``_future_A``: New future value of ``A``
    * ``_future_time``: Timestamp at which new ``A`` should take effect

.. py:function:: StableSwap.stop_ramp_A()

    Stops ramping ``A`` up or down and sets ``A`` to current ``A``.


Trade Fees
----------

.. py:function:: StableSwap.commit_new_fee(_new_fee: uint256, _new_admin_fee: uint256)

    Commits new pool and admin fees for the pool. These fees do not take immediate effect.

    * ``_new_fee``: New pool fee
    * ``_new_admin_fee``: New admin fee (expressed as a percentage of the pool fee)

.. note::
    Both the pool ``fee`` and the ``admin_fee`` are capped by the constants ``MAX_FEE`` and ``MAX_ADMIN_FEE``, respectively. By default ``MAX_FEE`` is set at 50% and ``MAX_ADMIN_FEE`` at 100% (which is charged on the ``MAX_FEE`` amount).

.. py:function:: StableSwap.apply_new_fee()

    Applies the previously committed new pool and admin fees for the pool.

    .. note::
        Unlike ownership transfers, pool and admin fees may be set more than once.

.. py:function:: StableSwap.revert_new_parameters()

    Resets any previously committed new fees.

.. py:function:: StableSwap.admin_balances(i: uint256) -> uint256

    Get the admin balance for a single coin in the pool.

    * ``i``: Index of the coin to get admin balance for

    Returns the admin balance for coin ``i``.

.. py:function:: StableSwap.withdraw_admin_fees()

    Withdraws and transfers admin fees of the pool to the pool owner.

.. py:function:: StableSwap.donate_admin_fees()

    Donates all admin fees to the pool's liquidity providers.


Kill a Pool
-----------

.. py:function:: StableSwap.kill_me()

    Pause a pool by setting the ``is_killed`` boolean flag to ``True``.

    This disables the following pool functionality:
    * ``add_liquidity``
    * ``exchange``
    * ``remove_liquidity_imbalance``
    * ``remove_liquidity_one_coin``

    Hence, when paused, it is only possible for existing LPs to remove liquidity via ``remove_liquidity``.

.. py:function:: StableSwap.unkill_me()

    Unpause a pool that was previously paused, re-enabling exchanges.
