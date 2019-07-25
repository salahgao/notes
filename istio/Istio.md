# Istio


## ʲô�Ƿ�������

��������Service Mesh���������ڽ�������ͨѶ�Ļ�����ʩ�㡣���������ִ���ԭ��Ӧ�ó���ĸ��ӷ����������ɿ��ش�������ʵ���ϣ�Service Mesh ͨ����ͨ��һ���������������Sidecar proxy������Ӧ�ó�����벿����һ����ʵ�֣��������֪Ӧ�ó�����

��������Service Mesh���������ͨ����������������ЩӦ�ó����΢���������Լ�Ӧ��֮��Ľ��������Ź�ģ�͸����Ե���������������Խ��Խ�������͹�������������������֡����ؾ��⡢���ϻָ���ָ���ռ��ͼ���Լ�ͨ�����Ӹ��ӵ���ά�������� A/B ���ԡ���˿ȸ���������������ʿ��ƺͶ˵�����֤�ȡ�


## ʲô��Istio

Istio��Google/IBM/Lyft���Ͽ����Ŀ�ԴService Mesh��Ŀ��Istio�������ӡ����������ƺ͹۲����

Istio �ṩ��һ�������Ľ��������ͨ��Ϊ�������������ṩ��Ϊ����Ͳ�������������΢����Ӧ�ó���Ķ���������

## ΪʲôҪʹ�� Istio��

Istio �ṩһ�ּ򵥵ķ�ʽ��Ϊ�Ѳ���ķ��������磬��������и��ؾ��⡢�������֤����صȹ��ܣ�ֻ��Ҫ�Է���Ĵ������һ�����Ҫ���κθĶ�����Ҫ�÷���֧�� Istio��ֻ��Ҫ�����Ļ����в���һ������� sidecar ����ʹ�� Istio ����ƽ�湦�����ú͹����������΢����֮�����������ͨ�ţ�

- HTTP��gRPC��WebSocket �� TCP �������Զ����ؾ��⡣
- ͨ���ḻ��·�ɹ������ԡ�����ת�ƺ͹���ע�룬���Զ�������Ϊ����ϸ���ȿ��ơ�
- �ɲ���Ĳ��Բ������ API��֧�ַ��ʿ��ơ��������ƺ���
- �Գ��뼯Ⱥ��ںͳ����������������Զ�����ָ�ꡢ��־��¼��׷�١�
- ͨ��ǿ��Ļ�����ݵ���֤����Ȩ���ڼ�Ⱥ��ʵ�ְ�ȫ�ķ����ͨ�š�

Istio ּ��ʵ�ֿ���չ�ԣ�������ֲ�������

## �ܹ�

Istio ���������߼��Ϸ�Ϊ**����ƽ��**��**����ƽ��**��

- **����ƽ��**��һ���� sidecar ��ʽ��������ܴ���Envoy����ɡ���Щ������Ե��ںͿ���΢���� Mixer ֮�����е�����ͨ�š�

- **����ƽ��**�����������ô�����·���������������ƽ������ Mixer ��ʵʩ���Ժ��ռ�ң�����ݡ�

��ͼ��ʾ�˹���ÿ�����Ĳ�ͬ�����
![�ܹ�](./images/arch.svg)

- **Envoy**��Istio ʹ�� Envoy �������չ�汾��Envoy ���� C++ �����ĸ����ܴ������ڵ���������������з����������վ�ͳ�վ������
- **Mixer**��Mixer ��һ��������ƽ̨������������ڷ���������ִ�з��ʿ��ƺ�ʹ�ò��ԣ����� Envoy ��������������ռ�ң�����ݡ�
- **Pilot**��Pilot Ϊ Envoy sidecar �ṩ�����ֹ��ܣ�Ϊ����·�ɣ����� A/B ���ԡ���˿ȸ����ȣ��͵��ԣ���ʱ�����ԡ��۶����ȣ��ṩ���������ܡ�
- **Citadel**��Citadel ͨ��������ݺ�ƾ֤������ǿ��ķ����������û������֤��
- **Galley**��Galley ���������� Istio ����ƽ�������������֤�û���д�� Istio API ���á�����ʱ������ƣ�Galley ���ӹ� Istio ��ȡ���á� ����ͷ�������Ķ������Ρ�


## Istio Dashboard - Naftis

��Ϊ������ʩ�㣬Istio������ķ���������������ʹ��Istio���з�������ʱ����������ͨ��istioctl��kubectl�������ն��н��в��������ַ�ʽĿǰ����һЩ���⣬�������£�
1. IstioҪ���û���������istioctl���ߵ�������ָ��нϸߵ�ѧϰ�ɱ���
2. Istio���з�������ʱ��Ҫ��yaml�����ļ��������ǳ��Ӵ�������ú͹�����Щ�����ļ���Ҳ�Ǹ����⡣
3. Istio��istioctl����û���û�Ȩ�޵�Լ��������һ����ȫ�������޷���Ӧ��˾�ϸ��Ȩ�޹�������
4. Istio��istioctl���߲�֧������ع���������ִ��������������£��޷����ٻع�����һ����ȷ�汾��

Ϊ�˽����Щ���⣬С��ΪIstio�з�����һ���Ѻ����õ�Dashboard - Naftis��

> Naftis��Ϊˮ�֣���Istio���������⾳���ϡ���Ϊdashboard��Naftis��ʹ�û���ˮ��һ�������ƿغ͹���Istio��

GitHub��ַ��https://github.com/XiaoMi/naftis

> Naftisͨ������ģ��ķ�ʽ�������û������ɵ�ִ��Istio�����û������� Naftis�ж����Լ�������ģ�壬��ͨ�������������쵥����������ʵ�����Ӷ���ɸ��ַ��������ܡ�

Naftis�ṩ���������ԣ�

- ������һЩ���õļ��ָ�꣬����40X��50X�������Ƶȡ�
- �ṩ�˿ɶ��Ƶ�����ģ���֧�֡�
- ֧�ֻع�ָ��ĳһ����
- �ṩ��Istio״̬��Ϲ��ܣ���ʵʱ�鿴Istio��Services��Pod״̬��
- ���伴�ã�ͨ��kubectlָ��һ������

## Rancher + Istio

Rancher��һ����Դ����ҵ��Kubernetes����ƽ̨��ʵ����Kubernetes��Ⱥ�ڻ����+�����������ĵļ��в��������

����Rancher�û�ϲ��Rancherƽ̨��ԭ�򣬾���Rancher�ù���Ͳ���Kubernetes����صĹ��ߺͼ�����ü���򵥣����û��ǲ��ص��Ļᱻ�ض����ƹ�Ӧ����������������Istio�����ǲ�ȡ��ͬ���ķ����������ڴ����û�ͬ�������顣

- ��Rancher 2.3 Preview�У�����Ϊ�û��ṩ��һ���򵥶��Ѻõ��û����棬��UI��ʹ�ù��߲˵�����������Istio��ϵͳ�ṩ�˺����Ĭ�����ã��û�Ҳ���Ը�����Ҫ�����޸ġ�
- Ϊ�˼��������Istio��Ҫע��Envoy sidecar����Rancher 2.3 Preview���У��û�����Ϊÿ���ռ�����ע���Զ�sidecar��һ������ѡ�����ѡ�Rancher�Ὣsidecar����ע�뵽ÿ���������ص��С�
- Rancher����Istio�İ�װ�����ã�������һ��֧��Kiali���Ǳ��̣�����������ң��Ŀ��ӻ���Ȼ����Jaeger����׷�٣����������Լ���Prometheus��Grafana�������ڸ߼���ص�ʵ����ͬ����
- �������Զ�sidecarע��������ռ��в��������غ���������ת��Istio�˵�Ŀ¼���۲�΢����Ӧ�ó����������
- ���Kiali��Jaeger��Prometheus����Grafana����������ÿ��������Ӧ���û����棬�������������ҵ���ϸ��Ϣ��ѡ�



## ���ٿ�ʼ

### [�� Kubernetes �п��ٿ�ʼ](https://istio.io/zh/docs/setup/kubernetes/install/kubernetes/)

��װIstio�������ݲ���Ҫ��װӦ��

1. ʹ�� kubectl apply ��װ Istio ���Զ�����Դ���壨CRD��

```
$ for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done
```

2. ����ģʽ�� mutual TLS

```
$ kubectl apply -f install/kubernetes/istio-demo.yaml
```

3. ȷ�ϲ�����

```
# kubectl get svc -n istio-system
NAME                     TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                                                                                                                                      AGE
grafana                  ClusterIP      10.43.164.25    <none>        3000/TCP                                                                                                                                     23h
istio-citadel            ClusterIP      10.43.166.140   <none>        8060/TCP,15014/TCP                                                                                                                           23h
istio-egressgateway      ClusterIP      10.43.35.2      <none>        80/TCP,443/TCP,15443/TCP                                                                                                                     23h
istio-galley             ClusterIP      10.43.150.39    <none>        443/TCP,15014/TCP,9901/TCP                                                                                                                   23h
istio-ingressgateway     LoadBalancer   10.43.175.89    <pending>     15020:30043/TCP,80:31380/TCP,443:31390/TCP,31400:31400/TCP,15029:31100/TCP,15030:31902/TCP,15031:31185/TCP,15032:31038/TCP,15443:31712/TCP   23h
istio-pilot              ClusterIP      10.43.214.79    <none>        15010/TCP,15011/TCP,8080/TCP,15014/TCP                                                                                                       23h
istio-policy             ClusterIP      10.43.170.89    <none>        9091/TCP,15004/TCP,15014/TCP                                                                                                                 23h
istio-sidecar-injector   ClusterIP      10.43.118.128   <none>        443/TCP                                                                                                                                      23h
istio-telemetry          ClusterIP      10.43.26.28     <none>        9091/TCP,15004/TCP,15014/TCP,42422/TCP                                                                                                       23h
jaeger-agent             ClusterIP      None            <none>        5775/UDP,6831/UDP,6832/UDP                                                                                                                   23h
jaeger-collector         ClusterIP      10.43.109.9     <none>        14267/TCP,14268/TCP                                                                                                                          23h
jaeger-query             ClusterIP      10.43.25.193    <none>        16686/TCP                                                                                                                                    23h
kiali                    ClusterIP      10.43.128.208   <none>        20001/TCP                                                                                                                                    23h
prometheus               ClusterIP      10.43.7.172     <none>        9090/TCP                                                                                                                                     23h
tracing                  ClusterIP      10.43.97.15     <none>        80/TCP                                                                                                                                       23h
zipkin                   ClusterIP      10.43.156.148   <none>        9411/TCP                                                                                                                                     23h

# kubectl get pods -n istio-system
NAME                                      READY   STATUS      RESTARTS   AGE
grafana-97fb6966d-dk5wl                   1/1     Running     0          23h
istio-citadel-7c7c5f5c99-f2spz            1/1     Running     0          23h
istio-cleanup-secrets-1.2.2-9wzq8         0/1     Completed   0          23h
istio-egressgateway-f7b8cc667-rdjvq       1/1     Running     0          23h
istio-galley-585fc86678-8njpb             1/1     Running     0          23h
istio-grafana-post-install-1.2.2-pxwln    0/1     Completed   0          23h
istio-ingressgateway-cfbf989b7-78cgr      1/1     Running     0          23h
istio-pilot-68f587df5d-46rt6              2/2     Running     0          6h32m
istio-pilot-68f587df5d-mdp9j              2/2     Running     0          23h
istio-policy-76cbcc4774-xs2h6             2/2     Running     2          23h
istio-security-post-install-1.2.2-6gsff   0/1     Completed   0          23h
istio-sidecar-injector-97f9878bc-bmnp4    1/1     Running     0          23h
istio-telemetry-5f4575974c-z22td          2/2     Running     2          23h
istio-tracing-595796cf54-dplhk            1/1     Running     0          23h
kiali-55fcfc86cc-cc9rb                    1/1     Running     0          23h
prometheus-5679cb4dcd-trxl4               1/1     Running     0          23h

```

ע�⣺���ǵ�ingressgateway EXTERNAL-IP �� <pending>������������أ�ֻ��ͨ������� NodePort ����ʹ�ö˿�ת�������з��ʡ�

### [Bookinfo Ӧ��](https://istio.io/zh/docs/examples/bookinfo/)

��װBookinfoӦ�á�

ʹ����������� http://$GATEWAY_URL/productpage ��Ϊû��EXTERNAL-IP����ʹ��NodePort���ҵĵ�ַ��http://[IP]:31380/productpage ���ˢ�¼���Ӧ�õ�ҳ�棬�ͻῴ�� productpage ҳ���л����չʾ reviews ����Ĳ�ͬ�汾��Ч������ɫ����ɫ�����λ���û����ʾ����

���Գ���**Ӧ��ȱʡĿ�����**

## ����-��������

### [������������](https://istio.io/zh/docs/tasks/traffic-management/request-routing/)
������˵����ν�����̬·�ɵ�����汾��΢����

### [����ע��](https://istio.io/zh/docs/tasks/traffic-management/fault-injection/)
������˵�����ע���ӳٲ�����Ӧ�ó���ĵ��ԡ�

### [����ת��](https://istio.io/zh/docs/tasks/traffic-management/traffic-shifting/)
��������ʾ����𲽽�������һ���汾��΢����Ǩ�Ƶ���һ���汾�����磬�����Խ������Ӿɰ汾Ǩ�Ƶ��°汾��

### [��������-���� Ingress ����](https://istio.io/zh/docs/tasks/traffic-management/ingress/)
�������������ʹ��Istio��������Istio���ڷ��������ⲿ��������
```
// �鿴 Sidecar ���Զ�ע��
kubectl get namespace -L istio-injection

```

## ����-��ȫ

### [HTTP ����ķ��ʿ���](https://istio.io/zh/docs/tasks/security/authz-http/)
Istio ���û��ڽ�ɫ�ķ��ʿ��Ʒ�ʽ���������ݺ�����Ϊ HTTP ���÷��ʿ��Ƶĸ������ڡ�

����ʧ����־��ʾ
```
[2019-07-24 08:13:03.541][22][debug][rbac] [external/envoy/source/extensions/filters/http/rbac/rbac_filter.cc:70] checking request: remoteAddress: 10.42.1.8:35818, localAddress: 10.42.0.18:9080, ssl: none, headers: ':authority', '139.219.9.241:31380'
':path', '/productpage'
':method', 'GET'
'upgrade-insecure-requests', '1'
'user-agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.142 Safari/537.36'
'accept', 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3'
'accept-encoding', 'gzip, deflate'
'accept-language', 'zh-CN,zh;q=0.9,en;q=0.8,zh-TW;q=0.7,da;q=0.6,is;q=0.5'
'x-forwarded-for', '10.42.0.0'
'x-forwarded-proto', 'http'
'x-request-id', '44ec4ca3-8959-9b7b-a23a-4597c955e4a7'
'x-istio-attributes', 'CkEKF2Rlc3RpbmF0aW9uLnNlcnZpY2UudWlkEiYSJGlzdGlvOi8vZGVmYXVsdC9zZXJ2aWNlcy9wcm9kdWN0cGFnZQpDChhkZXN0aW5hdGlvbi5zZXJ2aWNlLmhvc3QSJxIlcHJvZHVjdHBhZ2UuZGVmYXVsdC5zdmMuY2x1c3Rlci5sb2NhbAoqCh1kZXN0aW5hdGlvbi5zZXJ2aWNlLm5hbWVzcGFjZRIJEgdkZWZhdWx0CikKGGRlc3RpbmF0aW9uLnNlcnZpY2UubmFtZRINEgtwcm9kdWN0cGFnZQpOCgpzb3VyY2UudWlkEkASPmt1YmVybmV0ZXM6Ly9pc3Rpby1pbmdyZXNzZ2F0ZXdheS1jZmJmOTg5YjctNzhjZ3IuaXN0aW8tc3lzdGVt'
'x-b3-traceid', '29188100552e87bf9eb2b586e81379fd'
'x-b3-spanid', '9eb2b586e81379fd'
'x-b3-sampled', '1'
'content-length', '0'
'x-envoy-internal', 'true'
, dynamicMetadata: filter_metadata {
  key: "istio_authn"
  value {
  }
}

[2019-07-24 08:13:03.541][22][debug][rbac] [external/envoy/source/extensions/filters/http/rbac/rbac_filter.cc:114] enforced denied
@                                                                                                                                    ```

�޸� ServiceRoleBinding
```
apiVersion: "rbac.istio.io/v1alpha1"
kind: ServiceRoleBinding
metadata:
  name: bind-service-viewer
  namespace: default
spec:
  subjects:
  - user: "*"
  - properties:
      source.namespace: "istio-system"
  - properties:
      source.namespace: "default"
  roleRef:
    kind: ServiceRole
    name: "service-viewer"
```
����ͨ��


## ����-����

### [���ò��Լ��](https://istio.io/zh/docs/tasks/policy-enforcement/enabling-policy/)
�����񽲽�������� Istio ���Լ�鹦�ܡ�

## ��һ��

Service Mesh��������ҵ������������أ�һ������Ҫǿ�����ά֧�֣���Ҫ����ά����һ��������������һ������Ҫ�������׹��ߵ����ƣ����������������ֶ��������õȡ�

֮�����Ǳ��ֶ�Istio��Naftis��Rancher�����Ĺ�ע������̬��һ����������á�


## �ο�

[Istio�ĵ�](https://istio.io/zh/)

[С����ʽ��ԴIstio�������Naftis](https://mp.weixin.qq.com/s/Y2YBs4ENFWQTf7hEmsdi6g)

[��Istio���������м򵥣�Rancher�°汾����֧��Istio](https://mp.weixin.qq.com/s/YvCK7A-SpjjWd2zYpGqvqA)
