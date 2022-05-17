# AWS Storage Gateway

<aside>
💡 온프레미스에서 클라우드 스토리지에 액세스할 수 있도록 하이브리드 클라우드 스토리지 서비스

</aside>

### 예시

1. 온프레미스 데이터를 클라우드에 백업
2. 클라우드 스토리지에서 지원되는 온프레미스 파일 공유 사용
3. 온프레미스 애플리케이션에서 AWS의 데이터에 낮은 지연 시간으로 액세스 

### 유형 및 사용 사례

1. **Amazon S3 File Gateway**
    1. data file과 백업 이미지를 S3의 durable objects로 저장함
    2. S3에 있는 데이터에 **SMB** or **NFS**-based access 제공
2. **Amazon FSx File Gateway**
3. **Tape Gateway**
    
    > tape backup
    > 
4. **Volume Gateway**
    
    > block storage
    > 
    1. (Cache) 캐시 모드: 기본 데이터가 S3에 저장됨, 자주 액세스 하는 데이터는 로컬 캐시
    2. (Stored) 저장 모드: 기본 데이터가 로컬에 저장됨, S3에 비동기식으로 백업됨