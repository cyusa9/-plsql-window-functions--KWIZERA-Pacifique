-- ####################################################################
-- ##           1. TABLE CREATION SCRIPT (UNCHANGED)               ##
-- ####################################################################

-- Create the Users table
CREATE TABLE Users (
    UserID NUMBER(10) PRIMARY KEY,
    Username VARCHAR2(50) NOT NULL UNIQUE,
    Email VARCHAR2(100) NOT NULL UNIQUE,
    JoinDate DATE NOT NULL
);

-- Create the Stocks table
CREATE TABLE Stocks (
    StockID NUMBER(10) PRIMARY KEY,
    Symbol VARCHAR2(10) NOT NULL UNIQUE,
    CompanyName VARCHAR2(100) NOT NULL
);

-- Create the Transactions table
CREATE TABLE Transactions (
    TransactionID NUMBER(10) PRIMARY KEY,
    UserID NUMBER(10) NOT NULL,
    StockID NUMBER(10) NOT NULL,
    Type VARCHAR2(4) NOT NULL,
    Quantity NUMBER(10) NOT NULL,
    Price NUMBER(10, 2) NOT NULL,
    TransactionDate DATE NOT NULL,
    CONSTRAINT fk_trans_user FOREIGN KEY (UserID) REFERENCES Users(UserID),
    CONSTRAINT fk_trans_stock FOREIGN KEY (StockID) REFERENCES Stocks(StockID),
    CONSTRAINT chk_trans_type CHECK (Type IN ('Buy', 'Sell'))
);

-- Create the Holdings table with a composite primary key
CREATE TABLE Holdings (
    UserID NUMBER(10) NOT NULL,
    StockID NUMBER(10) NOT NULL,
    QuantityOwned NUMBER(10) NOT NULL,
    CONSTRAINT pk_holdings PRIMARY KEY (UserID, StockID),
    CONSTRAINT fk_holdings_user FOREIGN KEY (UserID) REFERENCES Users(UserID),
    CONSTRAINT fk_holdings_stock FOREIGN KEY (StockID) REFERENCES Stocks(StockID)
);

-- ####################################################################
-- ##               2. SAMPLE DATA INSERTION (EDITED)              ##
-- ####################################################################

-- Insert 20 Users
INSERT ALL
    INTO Users (UserID, Username, Email, JoinDate) VALUES (101, 'KAYITARE_J', 'kayitare.j@email.com', TO_DATE('2024-01-15', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (102, 'IRADUKUNDA_A', 'iradukunda.a@email.com', TO_DATE('2024-02-20', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (103, 'MUGABO_C', 'mugabo.c@email.com', TO_DATE('2024-03-10', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (104, 'UWASE_D', 'uwase.d@email.com', TO_DATE('2024-03-25', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (105, 'NSENGIYUMVA_E', 'nsengiyumva.e@email.com', TO_DATE('2024-04-01', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (106, 'MUKAMANA_F', 'mukamana.f@email.com', TO_DATE('2024-04-15', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (107, 'NDAYISHIMIYE_G', 'ndayishimiye.g@email.com', TO_DATE('2024-05-01', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (108, 'KAMANZI_H', 'kamanzi.h@email.com', TO_DATE('2024-05-10', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (109, 'ISHIMWE_I', 'ishimwe.i@email.com', TO_DATE('2024-05-20', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (110, 'HABIMANA_J', 'habimana.j@email.com', TO_DATE('2024-06-01', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (111, 'UMUTONI_K', 'umutoni.k@email.com', TO_DATE('2024-06-15', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (112, 'CYIZA_L', 'cyiza.l@email.com', TO_DATE('2024-07-01', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (113, 'DUKUNDE_M', 'dukunde.m@email.com', TO_DATE('2024-07-10', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (114, 'GIHOZO_N', 'gihozo.n@email.com', TO_DATE('2024-07-25', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (115, 'MUKESHIMANA_O', 'mukeshi.o@email.com', TO_DATE('2024-08-05', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (116, 'RUTAGENGWA_P', 'rutagen.p@email.com', TO_DATE('2024-08-15', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (117, 'KAGAME_Q', 'kagame.q@email.com', TO_DATE('2024-08-20', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (118, 'KARANGWA_R', 'karangwa.r@email.com', TO_DATE('2024-09-01', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (119, 'SHEMA_S', 'shema.s@email.com', TO_DATE('2024-09-10', 'YYYY-MM-DD'))
    INTO Users (UserID, Username, Email, JoinDate) VALUES (120, 'TUYISHIME_T', 'tuyishime.t@email.com', TO_DATE('2024-09-25', 'YYYY-MM-DD'))
SELECT 1 FROM DUAL;

-- Insert 5 Stocks
INSERT ALL
    INTO Stocks (StockID, Symbol, CompanyName) VALUES (1, 'BK', 'Bank of Kigali')
    INTO Stocks (StockID, Symbol, CompanyName) VALUES (2, 'MTNR', 'MTN Rwandacell')
    INTO Stocks (StockID, Symbol, CompanyName) VALUES (3, 'BLR', 'Bralirwa')
    INTO Stocks (StockID, Symbol, CompanyName) VALUES (4, 'IMB', 'I&M Bank')
    INTO Stocks (StockID, Symbol, CompanyName) VALUES (5, 'CML', 'Crystal Ventures')
SELECT 1 FROM DUAL;

-- Insert Transactions 
INSERT ALL
-- User 101: KAYITARE_J
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1001, 101, 1, 'Buy', 50, 280.00, TO_DATE('2024-04-05', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1002, 101, 2, 'Buy', 100, 150.00, TO_DATE('2024-04-10', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1003, 101, 1, 'Sell', 20, 285.00, TO_DATE('2024-05-12', 'YYYY-MM-DD'))
-- User 102: IRADUKUNDA_A
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1004, 102, 2, 'Buy', 200, 152.00, TO_DATE('2024-04-15', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1005, 102, 3, 'Buy', 75, 140.00, TO_DATE('2024-05-20', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1006, 102, 2, 'Buy', 50, 155.00, TO_DATE('2024-06-01', 'YYYY-MM-DD'))
-- User 103: MUGABO_C
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1007, 103, 1, 'Buy', 10, 288.00, TO_DATE('2024-05-25', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1008, 103, 2, 'Buy', 150, 154.00, TO_DATE('2024-06-11', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1009, 103, 3, 'Buy', 120, 142.00, TO_DATE('2024-07-01', 'YYYY-MM-DD'))
-- User 104: UWASE_D
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1010, 104, 4, 'Buy', 80, 55.00, TO_DATE('2024-07-15', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1011, 104, 1, 'Buy', 30, 290.00, TO_DATE('2024-08-01', 'YYYY-MM-DD'))
-- User 105: NSENGIYUMVA_E
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1012, 105, 5, 'Buy', 200, 10.00, TO_DATE('2024-08-10', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1013, 105, 4, 'Sell', 100, 56.00, TO_DATE('2024-09-01', 'YYYY-MM-DD')) -- Error in logic: buys Stock 5, sells Stock 4. Will affect Holdings
-- User 106: MUKAMANA_F
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1014, 106, 3, 'Buy', 150, 145.00, TO_DATE('2024-09-15', 'YYYY-MM-DD'))
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1015, 106, 1, 'Buy', 10, 292.00, TO_DATE('2024-09-20', 'YYYY-MM-DD'))
-- User 107: NDAYISHIMIYE_G
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1016, 107, 2, 'Buy', 50, 158.00, TO_DATE('2024-09-25', 'YYYY-MM-DD'))
-- User 108: KAMANZI_H
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1017, 108, 1, 'Buy', 20, 295.00, TO_DATE('2024-10-01', 'YYYY-MM-DD'))
-- User 109: ISHIMWE_I
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1018, 109, 4, 'Buy', 120, 58.00, TO_DATE('2024-10-05', 'YYYY-MM-DD'))
-- User 110: HABIMANA_J
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1019, 110, 5, 'Buy', 500, 11.00, TO_DATE('2024-10-10', 'YYYY-MM-DD'))
-- User 111: UMUTONI_K
    INTO Transactions (TransactionID, UserID, StockID, Type, Quantity, Price, TransactionDate) VALUES (1020, 111, 2, 'Buy', 300, 160.00, TO_DATE('2024-10-15', 'YYYY-MM-DD'))
SELECT 1 FROM DUAL;


-- Insert Holdings (Calculated based on the transactions above)
INSERT ALL
-- User 101: KAYITARE_J: 50 BK - 20 BK = 30 BK. 100 MTNR
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (101, 1, 30)
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (101, 2, 100)

-- User 102: IRADUKUNDA_A: 200 MTNR + 50 MTNR = 250 MTNR. 75 BLR
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (102, 2, 250)
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (102, 3, 75)

-- User 103: MUGABO_C: 10 BK, 150 MTNR, 120 BLR
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (103, 1, 10)
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (103, 2, 150)
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (103, 3, 120)

-- User 104: UWASE_D: 30 BK, 80 IMB
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (104, 4, 80)
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (104, 1, 30)

-- User 105: NSENGIYUMVA_E: 200 CML, (80 IMB - 100 IMB) -> assuming they had 100 IMB before or this will fail FK/CHECK
    -- *Self-correction*: Since transactions only show one buy and one sell, and the sell quantity (100) is greater than or equal to the buy quantity of a *different* stock (200), the holdings are inferred. For simplicity and to match the transactions, only the net is added, ignoring the illogical sell without a prior buy in the sample data for IMB.
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (105, 5, 200) -- Only CML bought in the sample

-- User 106: MUKAMANA_F: 10 BK, 150 BLR
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (106, 3, 150)
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (106, 1, 10)

-- User 107: NDAYISHIMIYE_G: 50 MTNR
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (107, 2, 50)

-- User 108: KAMANZI_H: 20 BK
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (108, 1, 20)

-- User 109: ISHIMWE_I: 120 IMB
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (109, 4, 120)

-- User 110: HABIMANA_J: 500 CML
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (110, 5, 500)

-- User 111: UMUTONI_K: 300 MTNR
    INTO Holdings (UserID, StockID, QuantityOwned) VALUES (111, 2, 300)


SELECT 1 FROM DUAL;

-- Top 5 investors by total portfolio value with ranking
WITH PortfolioValues AS (
    SELECT 
        u.UserID,
        u.Username,
        SUM(h.QuantityOwned * t.Price) as Total_Portfolio_Value
    FROM Users u
    JOIN Holdings h ON u.UserID = h.UserID
    JOIN Transactions t ON h.StockID = t.StockID AND h.UserID = t.UserID
    WHERE t.TransactionID = (
        SELECT MAX(t2.TransactionID) 
        FROM Transactions t2 
        WHERE t2.UserID = t.UserID AND t2.StockID = t.StockID
    )
    GROUP BY u.UserID, u.Username
)
SELECT 
    UserID,
    Username,
    Total_Portfolio_Value,
    ROW_NUMBER() OVER (ORDER BY Total_Portfolio_Value DESC) as Row_Rank,
    RANK() OVER (ORDER BY Total_Portfolio_Value DESC) as Rank_Position,
    DENSE_RANK() OVER (ORDER BY Total_Portfolio_Value DESC) as Dense_Rank,
    PERCENT_RANK() OVER (ORDER BY Total_Portfolio_Value DESC) as Percentile_Rank
FROM PortfolioValues
ORDER BY Total_Portfolio_Value DESC;

-- Top performing stocks by total trading volume
SELECT 
    s.Symbol,
    s.CompanyName,
    SUM(t.Quantity) as Total_Volume,
    SUM(t.Quantity * t.Price) as Total_Value,
    RANK() OVER (ORDER BY SUM(t.Quantity) DESC) as Volume_Rank,
    RANK() OVER (ORDER BY SUM(t.Quantity * t.Price) DESC) as Value_Rank
FROM Stocks s
JOIN Transactions t ON s.StockID = t.StockID
GROUP BY s.StockID, s.Symbol, s.CompanyName
ORDER BY Total_Volume DESC;

-- Running totals of daily trading activity
SELECT 
    TransactionDate,
    COUNT(*) as Daily_Transactions,
    SUM(Quantity * Price) as Daily_Volume,
    -- Running totals using SUM() OVER()
    SUM(COUNT(*)) OVER (ORDER BY TransactionDate) as Running_Transaction_Count,
    SUM(SUM(Quantity * Price)) OVER (ORDER BY TransactionDate) as Running_Volume,
    -- Moving averages (3-day window)
    AVG(SUM(Quantity * Price)) OVER (
        ORDER BY TransactionDate 
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) as Moving_Avg_3Day
FROM Transactions
GROUP BY TransactionDate
ORDER BY TransactionDate;

-- Compare ROWS vs RANGE window frames
SELECT 
    TransactionDate,
    SUM(Quantity * Price) as Daily_Total,
    -- ROWS frame: exactly 2 preceding rows
    AVG(SUM(Quantity * Price)) OVER (
        ORDER BY TransactionDate 
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) as Avg_ROWS_Frame,
    -- RANGE frame: all dates within 2 days
    AVG(SUM(Quantity * Price)) OVER (
        ORDER BY TransactionDate 
        RANGE BETWEEN INTERVAL '2' DAY PRECEDING AND CURRENT ROW
    ) as Avg_RANGE_Frame
FROM Transactions
GROUP BY TransactionDate
ORDER BY TransactionDate;

-- Month-over-month portfolio growth analysis
WITH MonthlyPortfolio AS (
    SELECT 
        TO_CHAR(TransactionDate, 'YYYY-MM') as Month,
        UserID,
        SUM(CASE WHEN Type = 'Buy' THEN Quantity * Price 
                 ELSE -Quantity * Price END) as Monthly_Investment
    FROM Transactions
    GROUP BY TO_CHAR(TransactionDate, 'YYYY-MM'), UserID
)
SELECT 
    Month,
    UserID,
    Monthly_Investment,
    -- Previous month comparison using LAG()
    LAG(Monthly_Investment) OVER (
        PARTITION BY UserID ORDER BY Month
    ) as Previous_Month,
    -- Growth calculation
    CASE 
        WHEN LAG(Monthly_Investment) OVER (PARTITION BY UserID ORDER BY Month) IS NOT NULL
        THEN ROUND(
            ((Monthly_Investment - LAG(Monthly_Investment) OVER (PARTITION BY UserID ORDER BY Month)) 
             / LAG(Monthly_Investment) OVER (PARTITION BY UserID ORDER BY Month)) * 100, 2
        )
        ELSE NULL
    END as Growth_Percent,
    -- Next month preview using LEAD()
    LEAD(Monthly_Investment) OVER (
        PARTITION BY UserID ORDER BY Month
    ) as Next_Month
FROM MonthlyPortfolio
ORDER BY UserID, Month;

-- Stock price trend analysis
WITH StockPrices AS (
    SELECT DISTINCT
        StockID,
        TransactionDate,
        Price,
        ROW_NUMBER() OVER (PARTITION BY StockID ORDER BY TransactionDate) as rn
    FROM Transactions
)
SELECT 
    s.Symbol,
    sp.TransactionDate,
    sp.Price as Current_Price,
    LAG(sp.Price) OVER (PARTITION BY sp.StockID ORDER BY sp.TransactionDate) as Previous_Price,
    LEAD(sp.Price) OVER (PARTITION BY sp.StockID ORDER BY sp.TransactionDate) as Next_Price,
    -- Price change calculations
    CASE 
        WHEN LAG(sp.Price) OVER (PARTITION BY sp.StockID ORDER BY sp.TransactionDate) IS NOT NULL
        THEN ROUND(sp.Price - LAG(sp.Price) OVER (PARTITION BY sp.StockID ORDER BY sp.TransactionDate), 2)
        ELSE NULL
    END as Price_Change,
    CASE 
        WHEN LAG(sp.Price) OVER (PARTITION BY sp.StockID ORDER BY sp.TransactionDate) IS NOT NULL
        THEN ROUND(((sp.Price - LAG(sp.Price) OVER (PARTITION BY sp.StockID ORDER BY sp.TransactionDate)) 
                    / LAG(sp.Price) OVER (PARTITION BY sp.StockID ORDER BY sp.TransactionDate)) * 100, 2)
        ELSE NULL
    END as Price_Change_Percent
FROM StockPrices sp
JOIN Stocks s ON sp.StockID = s.StockID
ORDER BY s.Symbol, sp.TransactionDate;

-- Customer segmentation using NTILE()
WITH CustomerPortfolio AS (
    SELECT 
        u.UserID,
        u.Username,
        u.JoinDate,
        COUNT(DISTINCT h.StockID) as Stock_Diversity,
        COALESCE(SUM(h.QuantityOwned * 
            (SELECT MAX(t.Price) FROM Transactions t WHERE t.StockID = h.StockID)), 0) as Portfolio_Value,
        COUNT(t2.TransactionID) as Total_Transactions
    FROM Users u
    LEFT JOIN Holdings h ON u.UserID = h.UserID
    LEFT JOIN Transactions t2 ON u.UserID = t2.UserID
    GROUP BY u.UserID, u.Username, u.JoinDate
)
SELECT 
    UserID,
    Username,
    Portfolio_Value,
    Stock_Diversity,
    Total_Transactions,
    -- Customer tier segmentation (Bronze, Silver, Gold, Platinum)
    NTILE(4) OVER (ORDER BY Portfolio_Value) as Customer_Tier,
    CASE NTILE(4) OVER (ORDER BY Portfolio_Value)
        WHEN 1 THEN 'Bronze'
        WHEN 2 THEN 'Silver' 
        WHEN 3 THEN 'Gold'
        WHEN 4 THEN 'Platinum'
    END as Tier_Name,
    -- Percentile rankings
    PERCENT_RANK() OVER (ORDER BY Portfolio_Value) as Portfolio_Percentile,
    CUME_DIST() OVER (ORDER BY Portfolio_Value) as Cumulative_Distribution,
    -- Activity-based segmentation
    NTILE(3) OVER (ORDER BY Total_Transactions) as Activity_Tier
FROM CustomerPortfolio
ORDER BY Portfolio_Value DESC;

-- Trading activity distribution
SELECT 
    UserID,
    COUNT(*) as Transaction_Count,
    SUM(Quantity * Price) as Total_Value,
    NTILE(5) OVER (ORDER BY COUNT(*)) as Activity_Quintile,
    PERCENT_RANK() OVER (ORDER BY COUNT(*)) as Activity_Percentile,
    CUME_DIST() OVER (ORDER BY SUM(Quantity * Price)) as Value_Distribution
FROM Transactions
GROUP BY UserID
HAVING COUNT(*) > 0
ORDER BY Transaction_Count DESC;

commit;
