# memo

## GPU operator

https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html#:~:text=Kubernetes%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC,%E5%AE%9F%E8%A1%8C%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82

Kubernetes クラスター内で GPU ワークロードを実行するすべてのワーカーノードまたはノードグループは、NVIDIA GPU ドライバーコンテナを使用するために、同じバージョンのオペレーティングシステムを実行する必要があります。または、ノードに NVIDIA GPU ドライバーを事前にインストールしておけば、異なるオペレーティングシステムを実行することもできます。

CPU ワークロードのみを実行するワーカー ノードまたはノード グループの場合、GPU オペレーターは CPU のみのワークロードのノードの構成や管理を実行しないため、ノードは任意のオペレーティング システムを実行できます。
