# Stock Project
This is a API project for managing `Stock`s, we can create, update, read, and delete `Stock`s.

![Spring Boot](https://img.shields.io/badge/Spring_Boot-F2F4F9?style=for-the-badge&logo=spring-boot "Spring Boot") ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white "Java") ![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white "Postman") ![Google Chrome](https://img.shields.io/badge/Google%20Chrome-4285F4?style=for-the-badge&logo=GoogleChrome&logoColor=white "Google Chrome")

## Frameworks and Languages
![Java v17](https://img.shields.io/badge/Java-v17-green "Java 17") ![Spring Boot](https://img.shields.io/badge/Spring%20Boot-v3.0.6-brightgreen "Spring Boot v3.0.6")

---
## Browser / Tools
![Google Chrome](https://img.shields.io/badge/Google%20Chrome-v112.0.5615.138-yellow "Google Chrome") ![Postman](https://img.shields.io/badge/Postman-v10.13.0-orange "Postman")
---

## Model
- ### Stock
    - ```java
      @Id
      @GeneratedValue(strategy = GenerationType.AUTO)
      private Integer stockId;
      ```
    - ```java
      @Column(unique = true)
      private String stockName;
      ```
    - ```java
      private Double stockPrice;
      ```
    - ```java
      private Integer stockOwnerCount;
      ```
    - ```java
      @Enumerated(EnumType.STRING)
      private StockType stockType;
      ```
    - ```java
      private Double stockMarketCap;
      ```
    - ```java
      private LocalDateTime stockBirthTimeStamp;
      ```
- ### StockType (Enum)
    - `FMCG`
    - `IT`
    - `HEALTH`
---
## Dataflow
- ### End Points / Controllers
  - #### _Stock_
    `@RequestMapping(value = "/stock")`
    - `@GetMapping(value = "/type/{stockType}")`
    - `@GetMapping(value = "abovePrice/price/{price}/lowerData/date/{date}")`
    - `@GetMapping(value = "/cap/{capPercentage}")`
    - `@PostMapping(value = "/")`
    - `@PutMapping(value = "/marketCap/{marketCap}/id/{id}")`
    - `@PutMapping(value = "/stock/type/id")`
    - `@PutMapping(value = "/stock/{id}")`
    - `@DeleteMapping(value = "/ownerCount/{count}")`
- ### Services
  - #### _Stock_
    ```java
    public List<Stock> getStocksByType(StockType stockType)
    ```
    ```java
    public String addStocks(List<Stock> stockList)
    ```
    ```java
    ppublic List<Stock> getStocksAbovePriceAndLowerDate(Double price, String date)
    ```
    ```java
    public List<Stock> getAllStocksAboveMarketCap(Double capPercentage)
    ```
    ```java
    @Transactional
    public void updateMarketCap(Double marketCap, Integer id)
    ```
    ```java
    @Transactional
    public void deleteStocksBasedOnCount(Integer count)
    ```
    ```java
    @Transactional
    public void updateTypeById(StockType stockType, Integer id)
    ```
    ```java
    @Transactional
    public void updateStockById(Integer id, Stock myStock)
    ```
- ### Repository
    - _Stock_
        ```java
        @Repository
        public interface IStockRepository extends CrudRepository<Stock,Integer> {
          List<Stock> findByStockPriceGreaterThanAndStockBirthTimeStampLessThanOrderByStockName(Double price, LocalDateTime date);

          List<Stock> findBy();

          @Query(value = "select * from STOCK where STOCK_MARKET_CAP > :capPercentage" , nativeQuery = true)
          List<Stock> getAllStocksAboveMarketCap(Double capPercentage);

          @Modifying
          @Query(value = "update STOCK set STOCK_MARKET_CAP = :capPercentage where Stock_id = :id" , nativeQuery = true)
          void updateMarketCapById(Double capPercentage, Integer id);

          @Modifying
          @Query(value = "Delete from Stock where Stock_owner_count <= :clientCount" , nativeQuery = true)
          void deleteStocksBasedOnCount(Integer clientCount);

          @Modifying
          @Query(value = "update stock set STOCK_TYPE = :myType where Stock_id = :id", nativeQuery = true)
          void modifyStockTypeById( String myType,Integer id);

          @Modifying
          @Query(value = "update stock set stock_id = :stockId, stock_name = :stockName, stock_price= :stockPrice, stock_Birth_Time_Stamp =:stockBirthTimeStamp where stock_id = :id",nativeQuery = true)
          void updateStockById(Integer id, Integer stockId, String stockName, Double stockPrice, LocalDateTime stockBirthTimeStamp);
        }
        ```
- ### Database
    I have used `MySQL` database in this project. And used `SpringDataJPA`.
---
## Datastructures
- `ArrayList<>`
---
## Summary
This API is a `Spring Boot` project that is about managing `Stock`s. We can create, read, update, and delete `Stock`s in database. In this project request is sent from the client on HTTP in JSON body or from path variable and stored in object then response is sent back from the server by JSON format to the client.

