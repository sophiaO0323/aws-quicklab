# AWS-Quicklab 股市爬蟲
## 實施架構
<img width="749" alt="截圖 2025-04-08 16 18 20" src="https://github.com/user-attachments/assets/ed6b43ee-db9b-4ad9-a8cf-0ff08e0d0e81" />

## 步驟1：建立S3 Bucket
### 用途：存放股票資料
1. 進入aws consoel
2. 進入s3點選 [Create bucket]

![image](https://github.com/user-attachments/assets/bb3002b8-0539-43bb-b9d8-7c409f44c1f9)

3. 為自己的buket取名字

![image](https://github.com/user-attachments/assets/9d9f90a9-ff52-4219-a9bd-5eb5a2d5ac0a)

4. 取消勾選「Block all publick access」，並勾選下面的警告，表示您了解取消勾選後會使bucket跟object公開

![image](https://github.com/user-attachments/assets/fbbce094-537c-4034-b82f-c3c4d467da15)

5. 點擊create buket

![image](https://github.com/user-attachments/assets/dbc9ceb0-3ae1-4119-ab51-beb75f619b75)

## 步驟2：建立第一個Lambda
### 用途：抓證交所網頁資料並存入S3
1. 進入Lambda，點選[Create Lambda]

![image](https://github.com/user-attachments/assets/d93bb68c-c640-4884-a1e3-45622bc1acfd)

2. 輸入Function name(名稱自訂)

![image](https://github.com/user-attachments/assets/4445dbc8-32b2-47e9-8222-df71733d832a)

3. Runtime選擇Python3.13

![image](https://github.com/user-attachments/assets/085d261b-2c9f-4804-a0c9-a3c7cf8fa431)

4. 展開下方的Change default execution role
    選擇[Use an existing role]
    下面選擇LabRole
    最後點選[Create function]

![image](https://github.com/user-attachments/assets/e7b844cd-32f2-4415-b07c-a8c22c8ad7c7)

5. 點選[Upload from]

![image](https://github.com/user-attachments/assets/280d61e3-c4dc-4e3d-8483-561f110121c1)

6. 選擇上傳[.zip file]

![image](https://github.com/user-attachments/assets/23844390-c02a-4b95-b512-23715bf0b271)

7. 點選[Upload]，選擇lambda_1.zip的檔案

![image](https://github.com/user-attachments/assets/8ff11714-ee9f-4785-8fb7-ec7bde80bc78)

8. 確認選擇的檔案是否正確，點擊[Save]

![image](https://github.com/user-attachments/assets/7f03d3f7-624d-4889-998f-2ed632b7cea2)

9. 點選[Configuration]

![image](https://github.com/user-attachments/assets/069b47e0-6a4c-409a-be05-57cf6faf1d8d)

10. 點選[Edit]

[image](https://github.com/user-attachments/assets/609b940c-9f6f-4ea5-a44e-b51dd33717ea)

11. 更改Timeout為1分鐘後，下面點選[save]

![image](https://github.com/user-attachments/assets/3eeb9120-ae02-4431-a8bc-bdb33b0461f8)

12. 點選[Code]

![image](https://github.com/user-attachments/assets/ff36cfae-d6a6-4fe2-b33f-f2b750fad32b)

13. 程式碼第19行更改成自己的S3 Bucketname（可以到s3去複製）

![image](https://github.com/user-attachments/assets/b71a704b-5dc0-4a3a-b031-97dbc6c1dd39)

14. 點選左邊的[Deploy]

![image](https://github.com/user-attachments/assets/babfa83b-12a1-4f0c-b3bb-a8f7124f783b)

15. 點選[Test]，[creare new test event]

![image](https://github.com/user-attachments/assets/5f14d875-5d71-4004-9186-6d7570d1072a)

![image](https://github.com/user-attachments/assets/bfa181f0-5365-4372-9938-560c69ab62f7)

16. 對測試事件取名字後，[save]

![image](https://github.com/user-attachments/assets/ed5a496c-0c4a-4f3b-b3e6-4cd68480a003)

17. 再次點選[Test]

![image](https://github.com/user-attachments/assets/8568856e-3f59-4ce3-9788-1505adf52ec4)

18. 選擇剛剛建的測試事件

![image](https://github.com/user-attachments/assets/70330f23-51d0-40d9-ac9c-05e7732c022f)

19. 跑完測試後，output的結果

![image](https://github.com/user-attachments/assets/45bab91a-7b05-4493-a12d-fb252abf5b22)

20. 進入s3檢查是否有爬下來的資料

![image](https://github.com/user-attachments/assets/a165a8ff-fdcf-403e-bc7d-59c54599e589)

## 步驟3：建立DynamoDB
### 用途
1. 進入DynamoDB，點選[Create table]

![image](https://github.com/user-attachments/assets/70953dca-c2b2-4910-8994-1f88b8d55c7e)

2. 取一個Table，Partition key寫id，點選[Create table]

![image](https://github.com/user-attachments/assets/331e3579-91be-4b47-b2ab-cccee9680a98)
![image](https://github.com/user-attachments/assets/de801c65-5908-4e3f-a6f7-d82de717c3e7)

## 步驟4：建立第二個Lambda
1. 進入Lambda，點選[Create Lambda]

![image](https://github.com/user-attachments/assets/b74b03c2-8e19-45fa-8907-79e4f0242ae1)

2. 輸入Function name(名稱自訂)

![image](https://github.com/user-attachments/assets/03c46dc4-cb81-4bc3-9432-25e346cc6d0e)

3. Runtime選擇Python3.13

![image](https://github.com/user-attachments/assets/a7d01c58-4edd-45f3-a565-c3e9792f61cb)

4. 展開下方的Change default execution role
    選擇[Use an existing role]
    下面選擇LabRole
    最後點選[Create function]

![image](https://github.com/user-attachments/assets/fb8f6879-47db-49ad-b0c0-599babca6307)

5. 點選[Add trigger]

![image](https://github.com/user-attachments/assets/43dda8b3-9a89-4ea4-bced-f5e5a698e95b)

6. 選擇s3

![image](https://github.com/user-attachments/assets/8f132e1b-3ead-47fb-86c4-36c81bbf09ae)

7. 選擇步驟1建立的Bucket

![image](https://github.com/user-attachments/assets/92e475c3-7034-44d0-ab66-e8ab2dcd3b9d)

8. 最下面的勾選起來（確保 Lambda 函數的輸入和輸出使用不同的 S3 存儲桶，避免因寫入相同存儲桶而觸發遞迴調用，進而增加使用量與成本。）
最後點選[add]

![image](https://github.com/user-attachments/assets/1e365d0d-4530-4152-9c54-35029cf97942)

9. Lambda左邊有s3表示有成功新增trigger

![image](https://github.com/user-attachments/assets/cdf1bc98-fea9-4e7c-904b-501bbd70ee66)

10. 點選[Upload from]

![image](https://github.com/user-attachments/assets/fb2a55f0-2c57-42cc-8ac3-54f90c261347)

11. 選擇上傳[.zip file]

![image](https://github.com/user-attachments/assets/14a17f76-42a0-49f6-951b-e3bef8dfe8fe)

12. 點選[Upload]，選擇lambda_2.zip的檔案

![image](https://github.com/user-attachments/assets/75da15b9-a14d-452c-beeb-bd994961313d)

13. 確認選擇的檔案是否正確，點擊[Save]

![image](https://github.com/user-attachments/assets/54832639-a2f3-4c73-9de5-3dee2571e2e4)

14. 更改程式碼第12行更換成DynamoDB table name

![image](https://github.com/user-attachments/assets/f1942918-ab7a-4ceb-bcce-e0c8e65de335)

15. 點選左邊的[Deploy]

![image](https://github.com/user-attachments/assets/6e230941-bbbc-4365-9c53-59408b5264ae)

16. 點選[Test]，[creare new test event]

![image](https://github.com/user-attachments/assets/cff24bd4-8a4c-4c9b-bdca-a1c697c570f7)

![image](https://github.com/user-attachments/assets/ed12f488-bc05-4d1e-a009-0a420e89d33c)

17. 對測試事件取名字

![image](https://github.com/user-attachments/assets/96940cb0-e3a4-4a9b-b33b-a63b5a882cae)

18. 複製lambda_test.json內的測試資料
19. 第23行換成s3 bucket name，第30行換成object key

![image](https://github.com/user-attachments/assets/6e9012ef-a49d-44de-9d6d-a310cd7966f3)

20. object key是s3 bucket內的object name。
進入bucket，複製其中一個object name，或是點進去object內也有可以點選複製的

![image](https://github.com/user-attachments/assets/73172787-c586-49ca-b64b-b0ae80a1a743)

![image](https://github.com/user-attachments/assets/e9ae6d6e-ece0-4dcb-ae12-b173831035cd)

21. 確認兩個地方更改完成後，點選[save]

![image](https://github.com/user-attachments/assets/99b5727d-6aca-4d37-b554-4238f07bba5f)

22. 再次點選[Test]

![image](https://github.com/user-attachments/assets/6a649a11-c30a-406b-810b-80447b450082)

23. 選擇剛剛建的測試事件

![image](https://github.com/user-attachments/assets/0746e357-3c5d-4754-bb71-a80eddd53ead)

24. 跑完測試後，output的結果

![image](https://github.com/user-attachments/assets/a1c4fce7-e0f0-4bdf-aa02-e5f1eb4ce1c9)

25. 進入DynamoDB查看是否有資料，點選Explore items

![image](https://github.com/user-attachments/assets/fe242f5d-267c-4e2e-8b1f-ee0061a857cc)

26. 選擇你在步驟2建立的table

![image](https://github.com/user-attachments/assets/7bde5607-041d-4a8c-b7f8-794e4928adc7)

27. 有出現資料表示有成功將網站抓取的股票資料存入資料庫

![image](https://github.com/user-attachments/assets/7d4576e6-0bd1-4613-b6c5-25c2d5566b9d)


## 步驟5：正式進行爬蟲、解析資料並存到DynamoDB
1. 將剛剛因測試而建立的資料。全選後，點擊[Actions]，選擇Delete items

![image](https://github.com/user-attachments/assets/d710018d-f395-44bc-94ad-fca5aced9b4b)

2. 再來要設定串流。選擇Tables，並點進你創建的table

![image](https://github.com/user-attachments/assets/0d0ac35b-9f80-48c6-a31f-62a36d756b1f)

3. 點選Exports and streams設定串流

![image](https://github.com/user-attachments/assets/f6228da2-5d01-47c0-9ac0-1e8a05430030)

4. 在DynamoDB stream details，點選turn on

![image](https://github.com/user-attachments/assets/0fd8c35a-0701-4cc4-ada5-8e19dbe8ecfb)

5. 選擇New and old images後，[Turn on stream]

![image](https://github.com/user-attachments/assets/9b3f039f-e83a-47ad-930f-f2ff10ac82b5)

6. 回到第一個建立的Lambda，點選[Test]

![image](https://github.com/user-attachments/assets/edbeb632-7903-4f09-a858-0b62d246288c)

7. 爬蟲結果Succeeded後，回去DynamoDB

![image](https://github.com/user-attachments/assets/d2851fd5-4684-4a22-a634-df2d8fab565d)

8. 成功，若是沒有資料可以點一下重整

![image](https://github.com/user-attachments/assets/5212c768-1003-49c9-9151-b24afb609029)
