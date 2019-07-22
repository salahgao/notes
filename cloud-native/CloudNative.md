# ��ԭ����Cloud Native���Ķ���

Pivotal ����ԭ��Ӧ�õ�����ߣ����Ƴ��� Pivotal Cloud Foundry ��ԭ��Ӧ��ƽ̨�� Spring ��Դ Java ������ܣ���Ϊ��ԭ��Ӧ�üܹ��������ߺ�̽·�ߡ�

## Pivotal����Ķ���

����2015��Pivotal��˾��Matt Stineд��һ������
[Ǩ�Ƶ���ԭ��Ӧ�üܹ�](https://jimmysong.io/migrating-to-cloud-native-application-architectures/)
��С���ӣ�����̽������ԭ��Ӧ�üܹ��ļ�����Ҫ������

- ����12����Ӧ��
- ����΢����ܹ�
- �Է������ݼܹ�
- ����API��Э��
- ��������

## Pivotal�����Ķ���

Pivotal���� https://pivotal.io/cn/cloud-native ���µĶ��壺

��ԭ����һ�ַ��������ڹ��������г�������Ƽ���ģ�����Ƶ�Ӧ�á�

��ҵ��Ҫһ�����ڹ�����������ԭ��Ӧ�úͷ����ƽ̨�����Զ�ִ�в����� DevOps������������΢����������ȸ��

![CloudNative](./images/diagram-cloud-native.png)

- DevOps �����������Ա�� IT ��Ӫ֮��ĺ�����Ŀ�����Զ�ִ����������ͻ����ܹ��������̡���������һ���Ļ��ͻ������������п��١�Ƶ���Ҹ��ɿ��ع��������Ժͷ��������

- ��������ʹ�õ���Ӧ�ø�����׼�������󼴿ɷ����������صȴ��������������󷢲���ȴ�ά�������ڵ��¼������������÷�����Ϊ���ƽ���ɿ��������ҵ�����Ը��͵ķ���Ƶ��������������ػ�������û��ķ�����ֱ�������Ϊҵ�����̺���ҵ�������ز����ٵ���ɲ��֡�

- ΢�����ǽ�Ӧ����ΪС�ͷ��񼯺Ͻ��п����ļܹ�����������ÿ�����񶼿�ʵʩҵ���ܣ����Լ������������в�ͨ�� HTTP API ����ͨ�š�ÿ��΢���񶼿��Զ�����Ӧ���е�����������в�����������չ������������ͨ����Ϊ�Զ���ϵͳ��һ�������У������ڲ�Ӱ�����տͻ��������Ƶ����������ʹ���е�Ӧ�á�

- ���׼�������ȣ�������ͬʱ�ṩЧ�ʺ��ٶȡ���������ϵͳʵ��ʹ�ò���ϵͳ �������⻯����һ��������������֮����ж�̬���֣�ÿ������������Ψһ�Ŀ�д�ļ�ϵͳ����Դ���������ƻ������Ŀ����ϵͣ��ټ��ϵ���������еĸ߰�װ�ܶȣ�ʹ������Ϊ�������΢������������㹤�ߡ�

## RedHat�����Ķ���

RedHat���� https://www.redhat.com/zh/topics/cloud-native-apps ���������¶��壺

��ԭ��Ӧ���Ƕ�����С��ģ��ɢ��Ϸ���ļ��ϣ�ּ���ṩ�����Ͽɵ�ҵ���ֵ����������ں��û�������ʵ�ֳ����Ľ��������֮��ͨ����ԭ��Ӧ�ÿ����������Լ��ٹ�����Ӧ�ã��Ż�����Ӧ�ò�����ЩӦ��ȫ�������һ����Ŀ��������ҵ��Ҫ���ٶ�����Ӧ���û�������

��ι�����ԭ��Ӧ�ã�
- DevOps
- ΢����
- API
- ����


## CNCF����Ķ���

����2015��Google������������ԭ���������ᣨCNCF�������CNCF����ԭ����Cloud Native���Ķ�����������������棺

- Ӧ��������
- ����΢����ܹ�
- Ӧ��֧�������ı��ŵ���

����2018�꣬���Ž���������ԭ����̬�Ĳ���׳�����������Ƽ��㹩Ӧ�̶������˸û���ᣬ�Ҵ�Cloud Native Landscape�п��Կ�����ԭ�������ʳԭ�ȷ���ԭ��Ӧ�õĲ��֡�CNCF������еĻ�Ա�Լ����ɵ���ĿԽ��Խ�࣬�ö����Ѿ���������ԭ����̬�ķ�չ��CNCFΪ��ԭ�����������¶�λ��


������CNCF����ԭ�������¶��壨��Ӣ���գ���

> Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach.

> ��ԭ�����������ڸ���֯�ڹ����ơ�˽���ƺͻ���Ƶ����Ͷ�̬�����У����������пɵ�����չ��Ӧ�á�**��ԭ���Ĵ�����������������������΢���񡢲��ɱ������ʩ������ʽAPI��**

> These techniques enable loosely coupled systems that are resilient, manageable, and observable. Combined with robust automation, they allow engineers to make high-impact changes frequently and predictably with minimal toil.

> ��Щ�����ܹ������ݴ��Ժá����ڹ���ͱ��ڹ۲�������ϵͳ����Ͽɿ����Զ����ֶΣ���ԭ������ʹ����ʦ�ܹ����ɵض�ϵͳ����Ƶ���Ϳ�Ԥ����ش�����

> The Cloud Native Computing Foundation seeks to drive adoption of this paradigm by fostering and sustaining an ecosystem of open source, vendor-neutral projects. We democratize state-of-the-art patterns to make these innovations accessible for everyone.

> ��ԭ���������ᣨCNCF��������������ά��һ�����������Ŀ�Դ��̬ϵͳ�����ƹ���ԭ������������ͨ������ǰ�ص�ģʽ������������Щ����Ϊ�������á�

CNCF�����ַ��https://github.com/cncf/toc/blob/master/DEFINITION.md
