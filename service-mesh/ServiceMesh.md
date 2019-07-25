# Service Mesh

## Service Mesh����

Service Mesh ������ ���������񡱣���Ϊ�����ͨ�ŵĻ�����ʩ�㡣Buoyant ��˾�� CEO Willian Morgan ��������ƪ���� [WHAT��S A Service Mesh? AND WHY DO I NEED ONE?](https://buoyant.io/2017/04/25/whats-a-service-mesh-and-why-do-i-need-one/) �н�����ʲô�� Service Mesh��Ϊʲô��ԭ��Ӧ����Ҫ Service Mesh��

������ Willian Morgan �� Service Mesh �Ľ��͡�

> A Service Mesh is a dedicated infrastructure layer for handling service-to-service communication. It��s responsible for the reliable delivery of requests through the complex topology of services that comprise a modern, cloud native application. In practice, the Service Mesh is typically implemented as an array of lightweight network proxies that are deployed alongside application code, without the application needing to be aware.

����������ǣ�

> ��������Service Mesh���������ڽ�������ͨѶ�Ļ�����ʩ�㡣���������ִ���ԭ��Ӧ�ó���ĸ��ӷ����������ɿ��ش�������ʵ���ϣ�Service Mesh ͨ����ͨ��һ���������������Sidecar proxy������Ӧ�ó�����벿����һ����ʵ�֣��������֪Ӧ�ó�����

## Service Mesh���ص�

Service Mesh �����¼����ص㣺
- Ӧ�ó����ͨѶ���м��
- �������������
- Ӧ�ó����޸�֪
- ����Ӧ�ó��������/��ʱ����ء�׷�ٺͷ�����

Ŀǰ�������е� Service Mesh ��Դ��� Istio �� Linkerd ������ֱ���� kubernetes �м��ɣ����� Linkerd �Ѿ���Ϊ CNCF ��Ա��

## Service Mesh�ļܹ�

![Service Mesh�ļܹ�](./images/service-mesh.png)

Service Mesh ��Ϊ sidecar ���У���Ӧ�ó�����˵��͸��������Ӧ�ó�������������ͨ���������Զ�Ӧ�ó��������Ŀ��ƶ������� serivce mesh ��ʵ�֡�

## �ο�

https://jimmysong.io/posts/what-is-a-service-mesh/

https://buoyant.io/2017/04/25/whats-a-service-mesh-and-why-do-i-need-one/

