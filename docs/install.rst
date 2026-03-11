安装
=====

pip 安装
--------

.. code-block:: bash

    pip install finshare

源码安装
--------

.. code-block:: bash

    git clone https://github.com/finvfamily/finshare.git
    cd finshare
    pip install -e .

依赖要求
--------

- Python >= 3.8
- requests >= 2.28.0
- pandas >= 1.5.0
- pydantic >= 2.0.0

可选依赖
--------

- **yfinance** - 美股数据获取（使用 Yahoo Finance 数据源）

.. code-block:: bash

    # 安装美股支持
    pip install yfinance
