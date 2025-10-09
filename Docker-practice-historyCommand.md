

```
 2370  docker run -u O --priviledged --name jenkins -it -d -p 8181:8181 -p 50000:50000 \\n-v /var/run/docker.sock:/var/run/dicker.sock \\n-v $(which docker):/usr/bin/docker \\n-v /home/jenkins_home:/var/jenkins_home \\njenkins/jenkins:latest
 2371  ^[[200~docker run -u O --privileged --name jenkins -it -d -p 8181:8181 -p 50000:50000 \\n-v /var/run/docker.sock:/var/run/dicker.sock \\n-v $(which docker):/usr/bin/docker \\n-v /home/jenkins_home:/var/jenkins_home \\njenkins/jenkins:latest
 2372  docker run -u O --privileged --name jenkins -it -d -p 8181:8181 -p 50000:50000 \\n-v /var/run/docker.sock:/var/run/dicker.sock \\n-v $(which docker):/usr/bin/docker \\n-v /home/jenkins_home:/var/jenkins_home \\njenkins/jenkins:latest\n
 2373  docker ps
 2374  docker start
 2375  docker run
 2376  docker run -u 0 --privileged --name jenkins -d \\n  -p 8181:8080 -p 50000:50000 \\n  -v /var/run/docker.sock:/var/run/docker.sock \\n  -v $(which docker):/usr/bin/docker \\n  -v $HOME/Documents/jenkins_home:/var/jenkins_home \\n  jenkins/jenkins:lts
 2377  open -a Docker
 2378  docker ps
 2379  docker run -u 0 --privileged --name jenkins -d \\n  -p 8181:8080 -p 50000:50000 \\n  -v /var/run/docker.sock:/var/run/docker.sock \\n  -v $(which docker):/usr/bin/docker \\n  -v $HOME/Documents/jenkins_home:/var/jenkins_home \\n  jenkins/jenkins:lts
 2380  docker ps -a
 2381  docker start jenkins
 2382  docker rm -f jenkins
 2383  docker run -u 0 --privileged --name jenkins -d \\n  -p 8181:8080 -p 50000:50000 \\n  -v /var/run/docker.sock:/var/run/docker.sock \\n  -v $(which docker):/usr/bin/docker \\n  -v $HOME/Documents/jenkins_home:/var/jenkins_home \\n  jenkins/jenkins:lts
 2384  docker start jenkins
 2385  docker rm -f jenkins   # remove broken container\ndocker run -u 0 --privileged --name jenkins -d \\n  -p 8181:8080 -p 50000:50000 \\n  -v /var/run/docker.sock:/var/run/docker.sock \\n  -v $(which docker):/usr/bin/docker \\n  -v $HOME/Documents/jenkins_home:/var/jenkins_home \\n  jenkins/jenkins:lts\n
 2386  docker ps
 2387  docker logs -f 56f8a031291a
 2388  kubernetes get nodes
 2389  kubectl get nodes
 2390  java --version
 2391  java version
 2392  java
 2393  ps -ef| grep jenkins
 2394  java -version
 2395  brew install java
 2396  sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
 2397  echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc
 2398  export CPPFLAGS="-I/opt/homebrew/opt/openjdk/include"
 2399  java -version
 2400  brew cleanup openjdk
 2401  java -version
 2402  docker ps
 2403  which docker
 2404  PATH = /opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin\n
 2405  vim ~/Library/LaunchAgents/homebrew.mxcl.jenkins-lts.plist\n
 2406  launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.jenkins-lts.plist
 2407  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.jenkins-lts.plist
 2408  brew services list | grep jenkins
 2409  brew services list | grep jenkins-lts
 2410  cat ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2411  rm -rf ~/Library/LaunchAgents/homebrew.mxcl.jenkins-lts.plist
 2412  vim ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2413  launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2414  vim ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2415  launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2416  launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2417  brew services list | grep jenkins\n
 2418  brew services restart jenkins
 2419  jenkins started         raghavendracn ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist\n
 2420  launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist\n
 2421  launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist\n
 2422  brew services list | grep jenkins\n
 2423  docker pull node:16-alpine
 2424  echo $http_proxy
 2425  echo $https_proxy
 2426  docker pull hello-world
 2427  ifconfih
 2428  ifconfig
 2429  ip
 2430  vim ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2431  sudo vim ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2432  cat ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2433  launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist\nlaunchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist\n
 2434  launchctl bootout gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2435  launchctl bootstrap gui/$(id -u) ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2436  brew services list | grep jenkins\n
 2437  cat ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
 2438  npm install
 2439  brem install npm
 2440  brew install npm
 2441  brew cleanup node
 2442  npm test
 2443  cat /Users/raghavendracn/.npm/_logs/2025-08-21T02_45_30_503Z-debug-0.log
 2444  npm init -y
 2445  npm install --save-dev jest 
 2446  cat package.json
 2447  npm test
 2448  vim package.json
 2449  mkdir __tests__
 2450  echo "test('adds 1 + 2 to equal 3', () => { expect(1 + 2).toBe(3); });" > __tests__/sum.test.js
 2451  npm test
 2452  cat ~/.kube/config
 2453  ls
 2454  cd ..
 2455  ls
 2456  cd ansible
 2457  ls
 2458  cp ansible-master-key-demo.pem ../jenkins/
 2459  cd ../jenkins
 2460  ls
 2461  ssh -i "ansible-master-key demo.pem" ubuntu@ec2-44-251-75-193.us-west-2.compute.amazonaws.com
 2462  ls
 2463  ssh -i "ansible-master-key-demo.pem" ubuntu@ec2-44-251-75-193.us-west-2.compute.amazonaws.com
 2464  ssh -i "ansible-master-key-demo.pem" ubuntu@ec2-34-211-57-207.us-west-2.compute.amazonaws.com
 2465  vim install-argocd.sh
 2466  ssh -i "ansible-master-key-demo.pem" ubuntu@ec2-44-251-75-193.us-west-2.compute.amazonaws.com
 2467  ssh -i "ansible-master-key-demo.pem" ubuntu@ec2-34-211-57-207.us-west-2.compute.amazonaws.com
 2468  ls
 2469  cd Documents
 2470  ls
 2471  mkdir Docker
 2472  cd Docker
 2473  brew install argocd\n
 2474  argocd version --client\n
 2475  kubectl create namespace argocd\n
 2476  ls
 2477  cd Documents
 2478  ls
 2479  mkdir argocd
 2480  cd argocd
 2481  kubectl create namespace argocd\n
 2482  kubectl config current-context\nkubectl get nodes\n
 2483  kubectl auth whoami\n
 2484  kubectl auth can-i create namespaces\n
 2485  cd ..
 2486  ls
 2487  cd Kubernetes
 2488  ls
 2489  cd yaml_files
 2490  ls
 2491  kind create cluster name=shruthi --config=config.yml
 2492  kind create cluster --name=shruthi --config=config.yml
 2493  docker --version
 2494  kubectl get nodes
 2495  kind create cluster --name=shruthi --config=kind-cluster-config.yaml
 2496  ls
 2497  cat config.yml
 2498  ls -lrt
 2499  cd Kuberenetes_yaml
 2500  ls
 2501  cd ..
 2502  kind --version
 2503  kind create cluster --name=tws-cluster --config=kind-cluster-config.yaml
 2504  kind create cluster --name=tws-cluster --config=config.yaml
 2505  ls
 2506  kind create cluster --name=shruthi --config=config.yml
 2507  kubectl get nodes
 2508  sudo lsof -i :80
 2509  kill -9 503 83909
 2510  sudo lsof -i :80
 2511  kubectl get cluster
 2512  kind delete cluster --name=shruthi
 2513  cat config.yml
 2514  sudo lsof -i :8080
 2515  kill -9 63613
 2516  sudo lsof -i :8080
 2517  kill -9 86960
 2518  sudo lsof -i :8080
 2519  cat config.yml
 2520  cd ..
 2521  ls
 2522  cd kind_setup
 2523  ls
 2524  cat kind-cluster-config.yaml
 2525  cd .
 2526  cd ..
 2527  ls
 2528  cd yaml_files
 2529  ls
 2530  kind create cluster --name=shruthi --config=config.yml
 2531  docker images
 2532  kubectl get nodes
 2533  cd ..
 2534  ls
 2535  cd kind_setup
 2536  kind create cluster --name=tws-cluster --config=kind-cluster-config.yaml
 2537  docker ps
 2538  cd ..
 2539  ls
 2540  cd yaml_files
 2541  kind create cluster --name=shruthi --config=config.yml
 2542  vim config.yml
 2543  cd ..
 2544  ls
 2545  cd kind_setup
 2546  ls
 2547  cat kind-cluster-config.yaml
 2548  kind create cluster --name=shrithi --config=kind-cluster-config.yaml
 2549  kind delete cluster --name=shrithi
 2550  cd ..
 2551  ls
 2552  cd yaml_files
 2553  ls
 2554  vim config.yml
 2555  kind create cluster --name=shruthi --config=config.yml
 2556  kubectl cluster-info --context kind-shruthi
 2557  kubectl get nodes
 2558  kubectl get cluster
 2559  kubectl get clusters info
 2560  kubectl create namespace argocd\n
 2561  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml\n
 2562  kubectl get namespace
 2563  kubectl get pods -n argocd\n
 2564  watch kubectl get pods -n argocd\n
 2565  kubectl get pods -n argocd\n
 2566  kubectl get svc
 2567  kubectl port-forward svc/argocd-server -n argocd 8080:443\n
 2568  cd Documents
 2569  cd Kubernetes
 2570  cd yaml_files
 2571  kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo\n
 2572  cd ..
 2573  mkdir ELK
 2574  cd ELK
 2575  brew install elastic/tap/elasticsearch-full\n
 2576  elasticsearch
 2577  java --version
 2578  brew uninstall elasticsearch-full
 2579  brew install elasticsearch-full
 2580  elasticsearch\n
 2581  brew install openjdk@11\n
 2582  export CPPFLAGS="-I/opt/homebrew/opt/openjdk@11/include"
 2583  export JAVA_HOME=$(/usr/libexec/java_home -v 11)
 2584  elasticsearch\n
 2585  ls /opt/homebrew/Cellar/elasticsearch-full/7.17.4/libexec/jdk.app/Contents/Home/bin/\n
 2586  echo $ES_JAVA_HOME\n
 2587  export ES_JAVA_HOME=$(/usr/libexec/java_home -v 11)
 2588  echo $ES_JAVA_HOME\n
 2589  elasticsearch\n
 2590  brew install openjdk@11\n
 2591  brew reinstall openjdk@11
 2592  ^[[200~elasticsearch
 2593  elasticsearch\n
 2594  brew uninstall elasticsearch*
 2595  brew uninstall *elasticsearch*
 2596  brew install openjdk@11\n
 2597  sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk\n
 2598  java -version\n
 2599  brew tap elastic/tap
 2600  brew install elastic/tap/elasticsearch-full@7.17
 2601  brew install elastic/tap/elasticsearch-full
 2602  brew uninstall elasticsearch-full
 2603  brew install elastic/tap/elasticsearch-full@7.17
 2604  brew install elastic/tap/elasticsearch-full
 2605  brew services start elastic/tap/elasticsearch-full
 2606  /usr/libexec/java_home -V\n
 2607  brew install openjdk@11
 2608  sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
 2609  echo 'export ES_JAVA_HOME=$(/usr/libexec/java_home -v 11)' >> ~/.zshrc
 2610  source ~/.zshrc
 2611  /opt/homebrew/opt/elasticsearch-full@7.17/bin/elasticsearch
 2612  /opt/homebrew/opt/elasticsearch-full/bin/elasticsearch
 2613  brew services stop elastic/tap/elasticsearch-full\n
 2614  launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch-full.plist 2>/dev/null
 2615  rm ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch-full.plist
 2616  ES_JAVA_HOME=$(/usr/libexec/java_home -v 11) brew services start elastic/tap/elasticsearch-full
 2617  curl -X GET "localhost:9200/"
 2618  curl http://localhost:9200
 2619  curl -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.1.3-darwin-x86_64.tar.gz
 2620  ls
 2621  curl https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.1.3-darwin-x86_64.tar.gz.sha512 | shasum -a 512 -c -
 2622  ls
 2623  rm elasticsearch-9.1.3-darwin-x86_64.tar.gz\n
 2624  ls
 2625  curl -L --retry 3 -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.1.3-darwin-x86_64.tar.gz\n
 2626  ls
 2627  curl -s https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.1.3-darwin-x86_64.tar.gz.sha512 | shasum -a 512 -c -\n
 2628  tar -xzf elasticsearch-9.1.3-darwin-x86_64.tar.gz
 2629  cd elasticsearch-9.1.3/
 2630  ls
 2631  f1a8385c2772ccfc4fa5f9014510e14f447013775625c8ff8a28b062b99fb6a7fd9310f2c771376e5e0ff8b8b3a9817dbbfaef8241f43aae73166664fbd50250\n
 2632  f1a8385c2772ccfc4fa5f9014510e14f447013775625c8ff8a28b062b99fb6a7fd9310f2c771376e5e0ff8b8b3a9817dbbfaef8241f43aae73166664fbd50250  elasticsearch-9.1.3-darwin-x86_64.tar.gz\n
 2633  shasum -a 512 -c elasticsearch-9.1.3-darwin-x86_64.tar.gz.sha512\n
 2634  ls
 2635  ./bin/elasticsearch\n
 2636  curl http://localhost:9200/\n
 2637  ls jdk.app/Contents/Home/bin/java\n
 2638  export ES_JAVA_HOME="$(pwd)/jdk.app/Contents/Home"
 2639  ./bin/elasticsearch
 2640* cd ..
 2641* ls
 2642* cd ELK
 2643* echo 'export ES_JAVA_HOME=$HOME/Documents/ELK/elasticsearch-9.1.3/jdk.app/Contents/Home' >> ~/.zshrc
 2644* source ~/.zshrc
 2645* echo $ES_JAVA_HOME
 2646* $ES_JAVA_HOME/bin/java -version
 2647* ./bin/elasticsearch\n
 2648* cd elasticsearch-9.1.3
 2649* ls
 2650* ./bin/elasticsearch\n
 2651  bin/elasticsearch-create-enrollment-token -s node
 2652  ls
 2653  ./bin/elasticsearch-create-enrollment-token -s node
 2654  cd ..
 2655  ls
 2656  rm -rf *
 2657  ls
 2658  cd ..
 2659  ls
 2660  mkdir SRE
 2661  cd SRE
 2662  ls cpu
 2663  lscpu
 2664  top
 2665  uptime
 2666  top -h
 2667  docker network work ls
 2668  docker network ls
 2669  ls
 2670  cd ..
 2671  ls
 2672  cd Docker
 2673  ls
 2674  docker pull hello-world
 2675  docker run hello-world
 2676  docker ps
 2677  kind get cluster
 2678  kind get clusters
 2679  kind delete cluster --name *
 2680  kind delete cluster --name shruthi
 2681  kind dlete cluster --name tws-cluster
 2682  kind delete cluster --name tws-cluster
 2683  kind delete cluster --name istio-testing
 2684  docker ps
 2685  ls
 2686  docker run hello-world:latest
 2687  docker images
 2688  docker ps
 2689  docker pull hellow-world
 2690  docker pull hello-world
 2691  docker scout quickview hello-world
 2692  docker ps
 2693  docker run hello-world
 2694  docker ps
 2695  docker ps -a\n
 2696  docker rm $(docker ps -aq)
 2697  docker ps -a\n
 2698  docker rmi hello-world
 2699  ls
 2700  mkdir hello-docker
 2701  cd hello-docker
 2702  vi app.py
 2703  vi Dockerfile
 2704  docker build -t hello-python .
 2705  docker run hello-python
 2706  docker python
 2707  docker ps
 2708  docker ps -a
 2709  docker rm 4c881d269080
 2710  docker rmi hello-python
 2711  docker ps -a
 2712  cat Dockerfile
 2713  cat app.py
 2714  cd ..
 2715  mkdir mysql
 2716  cd mysql
 2717  \tdocker pull musql
 2718  docker pull mysql
 2719  docker scout quickview mysql
 2720  docker images
 2721  docker rmi abhishekf5/cicd-e2e
 2722  docker rmi abhishekf5/cicd-e2e:33
 2723  docker images
 2724  docker rmi node:16-alpine
 2725  docker rmi docker/getting-started:latest
 2726  docker rmi ubuntu:latest
 2727  docker rmi kindest/node
 2728  docker rmi kindest/node:v*
 2729  docker rmi kindest/node:v1.30.0
 2730  docker rmi kindest/node:v1.31.2
 2731  docker images
 2732  docker rmi node:latest
 2733  docker ragh1988/notes-app-k8s:latest
 2734  docker rmi ragh1988/notes-app-k8s:latest
 2735  docker rmi bitnami/mongodb:7.0.5-debian-11-r8 
 2736  docker rmi gcr.io/k8s-minikube/kicbase:v0.0.44
 2737  docker images
 2738  docker rmi notes-app-k8s:latest
 2739  docker rmi kicbase/stable:latest
 2740  docker rmi kicbase/stable:v0.0.47
 2741  docker rmi trainwithshubham/node-app:latest
 2742  docker images
 2743  docker rmi jenkins/jenkins:lts
 2744  docker rmi jenkins/jenkins:latest
 2745  docker images
 2746  docker rmi gcr.io/k8s-minikube/kicbase:v0.0.42
 2747  docker rmi kindest/node:<none>
 2748  docker rmi 9d05f134f12f
 2749  dockdr images
 2750  docker images
 2751  docker system prune -a
 2752  cls
 2753  clear
 2754  docker images
 2755  docker pull mysql
 2756  docker run -e MYSQL_ROOT_PASSWORD=ROOT mysql
 2757* docker ps
 2758* docker exec -it 1e56167229a9 -- bash
 2759* docker exec -it 1e56167229a9 bash
 2760* docker stop mysql
 2761* docker stop #!/bin/bash\n\n# ========================================\n# \U0001f9f9 Docker Cleanup Script - Safe Version\n# ========================================\n\necho "🚀 Starting Docker cleanup..."\n\n# Step 1: Stop all running containers\necho "🛑 Stopping running containers..."\ndocker stop $(docker ps -q) 2>/dev/null || echo "No running containers found."\n\n# Step 2: Remove all stopped containers\necho "🗑 Removing stopped containers..."\ndocker container prune -f\n\n# Step 3: Remove dangling (unused) images\necho "\U0001f9fd Removing dangling images..."\ndocker image prune -f\n\n# Step 4: Remove unused networks\necho "🌐 Removing unused networks..."\ndocker network prune -f\n\n# Step 5: (Optional) Remove all unused images\nread -p "❗ Do you want to remove ALL unused images? (y/n): " remove_all\nif [ "$remove_all" = "y" ]; then\n    echo "\U0001f9e8 Removing ALL unused images..."\n    docker image prune -a -f\nelse\n    echo "✅ Skipping full image cleanup."\nfi\n\n# Step 6: (Optional) Remove unused volumes\nread -p "❗ Do you want to remove unused volumes? (y/n): " remove_volumes\nif [ "$remove_volumes" = "y" ]; then\n    echo "📦 Removing unused volumes..."\n    docker volume prune -f\nelse\n    echo "✅ Skipping volume cleanup."\nfi\n\n# Step 7: Final cleanup summary\necho "✨ Final cleanup summary:"\ndocker system df\n\necho "✅ Docker cleanup completed successfully\n
 2762* docker ps
 2763* docker stop 1e56167229a9
 2764* docker ps
 2765  docker run -d -e MYSQL_ROOT_PASSWORD=root mysql
 2766* docker ps
 2767  docker exec -it b33f7106944b mysql -u root -p
 2768  docker images
 2769  docker rmi 90ec22e21be2
 2770  docker stop 90ec22e21be2
 2771  docker ps
 2772  docker stop b33f7106944b
 2773  docker rmi 90ec22e21be2
 2774  docker ps
 2775  docker images
 2776  docker rmi -f 90ec22e21be2
 2777  docker images
 2778  cd ..
 2779  mkdir java-project
 2780  cd java-project
 2781  git clone https://github.com/LondheShubham153/simple-java-docker.git
 2782  ls
 2783  cd simple-java-docker
 2784  ls
 2785  cat Dockerfile
 2786  mv Dockerfile Dockerfile-backup
 2787  ls
 2788  vim Dockerfile
 2789  cat Dockerfile
 2790  docker build -t java-app .
 2791  docker pull openjdk:17-jdk-alpine
 2792  docker pull eclipse-temurin:17-jdk\n
 2793  vim Dockerfile
 2794  cat Dockerfile
 2795  docker images
 2796  docker rmi 4ada0181d58d
 2797  docker images
 2798  docker build -t java-app .
 2799  docker images
 2800  docker run java-app
 2801  vim src/Main.java
 2802  cat src/Main.java
 2803  docker build -t java-app .
 2804  docker run java-app
 2805  cd ../..
 2806  git clone https://github.com/LondheShubham153/flask-app-ecs.git
 2807  ls
 2808  cd flask-app-ecs
 2809  ls
 2810  mv Dockerfile Dockerfile_backup
 2811  vim Dockerfile
 2812  docker build -t flask-app .
 2813  vim Dockerfile
 2814  cat Dockerfile
 2815  docker build -t flask-app .
 2816  vim Dockerfile
 2817  docker build -t flask-app .
 2818  cat Dockerfile
 2819  ls
 2820  vim Dockerfile
 2821  docker build -t flask-app .
 2822  docker images
 2823  docker rmi 00a3edf2d16a
 2824  docker ps
 2825  docker rmi d55838f3af51
 2826  docker images
 2827  docker rmi -f 00a3edf2d16a
 2828  cat Dockerfile
 2829  docker build -t flask-app .
 2830  docker run flask-app
 2831  ls
 2832  cat app.py
 2833  docker run -p 80:80 flask-app
 2834  ls
 2835  cat app.py
 2836  vim app.py
 2837  docker build -t flask-app .
 2838  docker run -p 80:80 flask-app
 2839  docker ps
 2840  docker run -d -p 80:80 flask-app
 2841  docker ps
 2842  docker logs f223f9635136
 2843  docker attacch f223f9635136
 2844  docker attach f223f9635136
 2845  docker stop f223f9635136
 2846  docker ps
 2847  docker start f223f9635136
 2848  docker ps
 2849  docker stop f223f9635136
 2850  docker ps
 2851  docker run -itd ubuntu
 2852  docker ps
 2853  docker stop a762bf43e276
 2854  docker ps
 2855  cd ..
 2856  docker network ls
 2857  docker network create mynetwork -d bridge
 2858  docker network ls
 2859  ls
 2860  git clone https://github.com/LondheShubham153/two-tier-flask-app.git
 2861  ls
 2862  cd two-tier-flask-app
 2863  ls
 2864  cat app.py
 2865  vim Dockerfile
 2866  cat Dockerfile
 2867  docker build -t two-tier-backend .
 2868  ls
 2869  docker ps
 2870  cd ..
 2871  ls
 2872  cd mysql
 2873  ls
 2874  cd ..
 2875  ls
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % 



```
