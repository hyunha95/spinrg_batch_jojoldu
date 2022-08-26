- @Configuration
    - Spring Batch의 모든 Job은 @Configuration으로 등록해서 사용한다.
- jobBuilderFactory.get("simpleJob")
    - simpleJob 이란 이름의 Batch Job을 생성한다.
- stepBuilderFactory.get("simpleStep1")
    - simpleStep1 이란 이름의 Batch Step을 생성한다.
    - jobBuilderFactory.get("simpleJob")와 마찬가지로 Builder를 통해 이름을 지정한다.
- .tasklet((contribution, chunkContext)) 
    - Step 안에서 수행될 기능들을 명시한다.
    - Tasklet은 Step안에서 단일로 수행될 커스텀한 기능들을 선언할때 사용한다.
    - 여기서는 Batch가 수행되면 log.info(">>>> This is Step1")가 출력되도록 한다.
   
Spring Batch에서 Job은 하나의 배치 작업 단위이다.   

<img width="866" alt="99E8E3425B66BA2713" src="https://user-images.githubusercontent.com/76119021/186567313-9d667ba4-3ce1-4e70-8722-fe89b54e4816.png">

Spring Batch에선 메타 데이터 테이블들이 필요하다.   
Spring Batch의 메타 데이터는 다음과 같은 내용들을 담고 있다.
- 이전에 실행한 Job이 어떤 것들이 있는지
- 최근 실패한 Batch Parameter가 어떤것들이 있고, 성공한 Job은 어떤것들이 있는지
- 다시 실행한다면 어디서 부터 시작하면 될지
- 어떤 Job에 어떤 Step들이 있었고, Step들 중 성공한 Step과 실패한 Step들은 어떤것들이 있는지 
   
BATCH_JOB_INSTANCE 테이블은 Job Parameter에 따라 생성되는 테이블이다. Spring Batch가 실행될 때 외부에서 받을 수 있는 파라미터 이다.   
같은 Batch Job이라도 Job Parameter가 다르면 BATCH_JOB_INSTANCE에는 기록되며, Job Parameter가 같다면 기록되지 않는다.

