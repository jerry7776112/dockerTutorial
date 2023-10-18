# dockerTutorial
## 專案名稱: dockerTutorial - NOTE
## 參考影片:**[TechWorld with Nana - Docker Tutorial for Beginners](https://youtu.be/3c-iBn73dDE?si=v0oP-u3dNs4dTmih)**

## What is a Container and What problems does it solve?(docker概念說明)
### What is a Container(concept)?
* A way to **package** application with **all** the **necessary dependencies** and configuration. (Container 是將應用程式及所需要的內容打包再套件內的方法)
*	Portable artifact, easily shared and moved around(可輕鬆分享及移植在其他環境)
*	Make development and deployment more efficient(可更有效率的部署)

### Container Repository
* 存放Container的地方，而一般公司則會有所謂自己的private repositories(私人存放)儲存私人的container的地方。

### Public repository for Docker
* DockHub: docker 官方所提供的公開存放container的網站，可在這裡找到任何應用程式container

### 傳統開發會遇到的問題:
*	Installation process different on each OS environment
*	Many steps where something could go wrong
*	Developer(撰寫相關說明文件)>Operations(根據文件進行操作設定部屬)
*	Configuration on the server needed，這樣可能會遇到一些版本不相容的問題
*	Misunderstandings(Developer與Operations認知理解可能不一樣，導致問題錯誤產生)，而誤解產生就需要溝通，一來一回的溝通會耗費很多時間，降低效率。

### 使用container(容器)開發:
* 不須直接在OS上安裝任何應用程式搭建環境，容器為一個與系統隔離的環境。(own isolated environment)
*	Packaged with all needed configuration
*	One command to install the app
*	Run same app with different version(在本機環境上執行相同應用程式的不同版本，而不會發生任何衝突)
*	不會因為OS不同而有所不同，使得開發環境會比使用傳統開發的方式更有效率且更簡單。
*	Developers and Operations work together to package the application in a container
*	No environmental configuration needed on server – except Docker Runtime(因為相關套件環境已經封裝在container中，執行docekr命令即可使用)

### What is a Container(technology)?
*	Layers of images: container是由images所組成，會有一層又一層堆疊的images。
*	Mostly Linux Base Image, because small in size(images中都會有最基礎且容量小的linux 在最底層) ex: alpine:3.10
*	Application image on top.在最高層   ex: postgres:10.10
*	其他的相關應用程式會在最高層和最低層之間。

### Docker Image & Docker Container 差別:
#### Docker
Docker Image:
* The actual package
* Artifact, that can be moved around 

Docker Container:
* Actually start the application
* Container environment is created

Docker vs Virtual Machine:
* Both are virtualization tools
* Docker(Applications, use local OS Kernel, because they have not OS Kernel)
* Size: Docker image much smaller
* Speed: Docker containers start and run much fast

#### VM
* VM(Applications, OS Kernel)
* Size: VM much big
* Compatibility: VM of any OS can run on any OS host
    * Docker on OS level
    * Different levels of abstractions
    * Why linux-based docker containers don’t run Windows
* Operating Systems have 2 Layers(Applications(2.Layer), OS Kernel(1.Layer), Hardware).
* They use same Linux Kernel, but implemented different application on top.

#### 補充
Difference Image and Container:
*	Container(File system, environment configs, application image, port(5000)) is a running environment for image.
*	application image: postgres, redis, mongo,…..
*	port binded: talk to application running inside of container
*	virtual file system

Container Port vs Host Port
*	Multiple containers can run on your host machine.
*	Your laptop has only certain ports available.
*	Conflict when same port on host machine.

#### 實作
* Docker Main Command Tutorial
    * 實作教學: **[dockerMainCommand.pdf](https://github.com/jerry7776112/dockerTutorial/blob/main/dockerMainCommand.pdf)**  
* Create Docker Network & Run Multiple Containers
    * 實作教學: **[CreateNetwork.pdf](https://github.com/jerry7776112/dockerTutorial/blob/main/CreateNetwork.pdf)**   
* Dockerfile - Building Docker Image
    * 實作教學: **[DockerfileBuildingDockerImage.pdf](https://github.com/jerry7776112/dockerTutorial/blob/main/DockerfileBuildingDockerImage.pdf)**
* Push docker image to AWS ECR & Deploy our containerized app
    * 實作教學: **[deployToAWSecr.pdf](https://github.com/jerry7776112/dockerTutorial/blob/main/deployToAWSecr.pdf)**

#### Docker Main Command
1. 下載 images
```docker pull <images name>```
2. 啟動新的 container & 直接 pull images 後啟動 container
```docker run <images name>```
3. 啟動另一個新的容器(d就是分離的意思)
```docker run –d```
4. 綁定 image 端口
```docker run-p<localPort>:<containerPort> <image>```
5. 綁定 image 端口並為 container 命名
```docker run-p<localPort>:<containerPort> <named> <image>```
6. 指定啟動未運行的 container
```docker start <id>```
7. 指定停止運行中的 container
```docker stop <id>```
8. 列出當前運行中的 container
```docker ps```
9. 列出當前所有存在的 container (不論是否運行中)
```docker ps –a: ```
10. 查看 container 的狀態資訊
```docker logs <Container ID or Names>: ```
11. 與 container 終端機互動
```docker exec –it <Container ID>```
12. 建立自己的image 
```docker build -t <image_name:tag> .```
t: 命名 
. :當前目錄
ex: docker build -t my-app:1.0 .
13. 刪除 container
```docker rm <container ID>```
14. 刪除 image
```docekr rmi <image name>```
15. 離開docker終端機
```exit```
16. 執行.yaml
```docker compose -f <.yaml> up```
-f : 指定要執行的檔案
up : 啟動
ex: docker compose -f mongo.yaml up
17. 關閉.yaml
```docker compose -f <.yaml> down```
-f : 指定要執行的檔案
down : 關閉
ex: docker compose -f mongo.yaml down
