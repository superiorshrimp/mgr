# Praca magisterska

**PDF:** https://github.com/superiorshrimp/mgr/blob/main/praca_magisterska.pdf

**Tytuł:** Równoległe i rozproszone metaheurystyki optymalizacyjne z desynchronizacją

**Streszczenie:** Synchronizacja stanu wiedzy między rozproszonymi węzłami obliczeniowymi w równoległym
algorytmie optymalizacyjnym może powodować znaczące opóźnienia w wykonaniu. Wprowa
dzenie desynchronizacji przyspiesza działanie, jednak może doprowadzić do uzyskania gor
szych wyników samego algorytmu. Przedstawiono implementację Evolutionary Multi-agent
System z desynchronizacją. Jest to realizacja metaheurystyki optymalizacyjnej, przebadanie
efektywności której jest celem tej pracy. Sprawdzono jej wydajność na dużej liczbie węzłów
obliczeniowych, wykorzystując do tego infrastrukturę centrum Cyfronet. Wyniki pokazują
poprawę w porównaniu do standardowej równoległej implementacji algorytmu.

**Title:** Parallel and distributed optimization metaheuristics with desynchronization

**Abstract:** The synchronization of knowledge states among distributed computing nodes in parallel
optimization algorithm can cause significant execution delays. Introducing desynchroniza
tion accelerates performance, but may also lead to worse algorithm results. This paper pre
sents an implementation of the Evolutionary Multi-agent System with desynchronization,
aiming to evaluate the effectiveness of this optimization metaheuristic. It’s performance was
tested across a large amount of computing nodes using the Cyfronet center’s infrastructure.
The results show an improvement compared to the standard parallel implementation of the
algorithm.

### Instalacja

lokalnie:
```
pip install "ray[default]"
pip install pika

ray start --head --port=6379 --dashboard-port=6380

docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
python islands_desync/geneticAlgorithm/utils/prepare_queues_2.py 

rabbitmqctl await_startup
rabbitmqctl add_user rabbitmq rabbitmq
rabbitmqctl set_user_tags rabbitmq rabbitmq
rabbitmqctl set_permissions -p / rabbitmq ".*" ".*" ".*"

# example run:
python islands_desync\minimal.py 3 4 8 CompleteTopology RandomSelect 1

ray stop
```

AWS EC2:
```
sudo yum update
sudo -y yum install docker
sudo usermod -a -G docker ec2-user
id ec2-user
newgrp docker
sudo systemctl enable docker.service
sudo systemctl start docker.service
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```

Cyfronet:
```
# set ip of rabbitmq deployment
sbatch run.sh
```
