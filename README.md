````markdown
# 🤖 Smart Trading Bot – Holberton Final Project (Year 1)

## 📌 Project Description
This project is a full-featured **crypto trading bot** developed from scratch as a final-year project for Holberton School (Year 1). The bot retrieves live market data via the **Bitget API**, analyzes it using technical indicators, and places buy/sell orders based on predefined strategies.

Later versions will support **AI/ML integration** for learning from trade history and adapting to market conditions.

---

## 🧠 Features (v1)
- Real-time market data fetching (candlesticks, positions, PnL)
- Technical analysis indicators (RSI, MACD, EMA...)
- Modular trading strategies (DCA, MACD+RSI, etc.)
- Order execution with Stop Loss / Take Profit
- Structured logging system
- Console-based interface
- Architecture prepared for future AI/ML upgrades

---

## 🧱 Architecture Overview

### 📦 Package Diagram
```mermaid
graph TD
    Bot[bot.py (Main Controller)]

    subgraph indicators
        RSI[RSI]
        MACD[MACD]
    end

    subgraph strategies
        DCA[DCA_Strategy]
        Combo[MACD_RSI_Combo]
    end

    subgraph data
        Fetcher[MarketDataFetcher]
        Serializer
        History[HistoricalData]
    end

    subgraph trading
        Orders[OrderExecutor]
        Active[PositionTracker]
        PnL[ProfitLossCalc]
    end

    subgraph logs
        Logger
    end

    subgraph ui
        UI[DisplayConsole]
    end

    subgraph ai
        AI_Module[Future AI/ML]
    end

    Bot --> indicators
    Bot --> strategies
    Bot --> data
    Bot --> trading
    Bot --> logs
    Bot --> ui
    Bot --> ai

    strategies --> indicators
    trading --> data
    ui --> logs
    ai --> logs
````

````

---

## 🧩 Class Diagram (Simplified)
```mermaid
classDiagram
    class MarketDataFetcher {
        +get_ohlcv(pair, timeframe)
        +get_open_positions()
    }

    class Indicator {
        <<abstract>>
        +compute(data)
    }
    class RSI {
        +compute(data)
    }
    class MACD {
        +compute(data)
    }

    class Strategy {
        <<abstract>>
        +evaluate_signals()
    }
    class DCA_Strategy {
        +evaluate_signals()
    }
    class MACD_RSI_Combo {
        +evaluate_signals()
    }

    class TradeExecutor {
        +place_order()
        +set_stop_loss()
    }

    class Logger {
        +log_event(event)
        +save_to_file()
    }

    class UI {
        +display_action(action)
        +show_trade_summary()
    }

    MarketDataFetcher --> RSI
    MarketDataFetcher --> MACD
    RSI --> Strategy
    MACD --> Strategy
    Strategy --> TradeExecutor
    TradeExecutor --> Logger
    Logger --> UI
````

````

---

## 🔁 Sequence Diagram (Typical Loop)
```mermaid
sequenceDiagram
    participant Bot
    participant DataFetcher
    participant RSI
    participant MACD
    participant Strategy
    participant Executor
    participant Logger
    participant UI

    Bot->>DataFetcher: get_ohlcv()
    DataFetcher-->>Bot: prices

    Bot->>RSI: compute(prices)
    RSI-->>Bot: rsi_value

    Bot->>MACD: compute(prices)
    MACD-->>Bot: macd_value

    Bot->>Strategy: evaluate_signals(rsi, macd)
    Strategy-->>Bot: buy/sell decision

    Bot->>Executor: place_order()
    Executor-->>Bot: confirmation

    Bot->>Logger: log_event()
    Logger-->>UI: display_action()
````

```

---

## 🚀 Technologies
- Python 3.11
- Bitget API (REST)
- `requests`, `json`, `datetime`, `pickle`
- Custom indicators (RSI, MACD)
- Mermaid.js for documentation

---

## 🔮 Future Work (v2/v3)
- AI/ML module for predictive models
- Fundamental news parsing and sentiment filtering
- Web dashboard for bot monitoring
- Strategy backtesting engine

---

## 👨‍💻 Author
Project made by Jules MOLEINS, student at Holberton School (France)

---

## 📜 License
MIT License – for educational and personal use
```
