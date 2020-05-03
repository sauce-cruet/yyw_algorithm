# 202. ������
### ԭ��
��дһ���㷨���ж�һ���� n �ǲ��ǿ�������
��������������Ϊ������һ����������ÿһ�ν������滻Ϊ��ÿ��λ���ϵ����ֵ�ƽ���ͣ�Ȼ���ظ��������ֱ���������Ϊ 1��Ҳ������ **����ѭ��** ��ʼ�ձ䲻�� 1����� ���Ա�Ϊ  1����ô��������ǿ�������
��� n �ǿ������ͷ��� True �����ǣ��򷵻� False ��

ʾ����
���룺19
�����true
���ͣ�

```
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

��Դ�����ۣ�LeetCode��
[����](https://leetcode-cn.com/problems/happy-number)��https://leetcode-cn.com/problems/happy-number

### 2�ֽⷨ
##### 1.ʹ�ù�ϣ���ж�ѭ��
```java
public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<>();
        set.add(n);
        while (true){
            n = create(n);
            if(n == 1)
                return true;
            if(set.contains(n))
                return false;
            set.add(n);
        }
    }

    private int create(int n) {
        int sum = 0;
        while (n != 0){
            sum += n % 10 * (n % 10);
            n /= 10;
        }
        return sum;
    }
```
˼·������
* ������Ŀ��˼�����һ�����������仯���տ���Ϊ1���ǿ����������򰴹���仯����������ѭ��������������Ҫ�ж��ڰ�����仯����ʱ��
    * �����Ƿ��Ϊ1������ǣ�����`true`
    * ������������Ƿ������ѭ��������ǣ�����`false`
* ���ȸ�������`int create(int n)`������Ŀ�任����õ�ת��������֡�ͨ��ѭ�������Ͻ�n��10ȡ����ƽ���Ӻ�`sum += n % 10 * (n % 10);`��Ȼ��`n /= 10;`ȥ������һ�����ֵļ��㡣
* ���������Ƕ����ֿ����Ƿ����ѭ��������ʹ��`Set<Integer> set = new HashSet<>();`����ų��ֹ������֡�
    * ���Ƚ�ԭ��������`set.add(n);`��
    * Ȼ��ʹ��ѭ����ģ�����ֱ仯�Ĺ��̡�`n = create(n);`�õ���һ��ת��������֣�
    * Ȼ���ж��Ƿ�Ϊ1������������ж��Ƿ�����ѳ������ֵļ����У��������`if(set.contains(n))`��˵��������ѭ��,����`false`�����򽫸����ַ��뼯���С�
* ������Ŀ�����������ѭ��һ����ͨ���������жϷ��ء�
* ʱ�临�Ӷ���ռ临�Ӷȶ�ȡ���������ֱ任�Ĺ����У����ж��ٸ���ͬ�����ֳ��֡�

���н����
* ִ����ʱ :2 ms, ������ Java �ύ�л�����51.98%���û�
* �ڴ����� :36.6 MB, ������ Java �ύ�л�����8.33%���û�

##### 2.ʹ�ÿ���ָ���ж�ѭ��
```java
public boolean isHappy2(int n){
        int slow = n, fast = create(n);
        while(fast != 1){
            if(fast == slow) return false; // ��ָ�������ָ�룬���˵���ڼ��������ѭ���ˣ�����֮�乹���˻���
            fast = create(create(fast));
            slow = create(slow);
        }
        return true;
    }

	private int create(int n) {
        int sum = 0;
        while (n != 0){
            sum += n % 10 * (n % 10);
            n /= 10;
        }
        return sum;
    }
```
˼·������
* ͬ���緽��һ�еķ����������������ж�
    * �任�������Ƿ�����ѭ��
    * ���������Ƿ��Ϊ1
* ���ֵı任��������ͬһ����������ǰ��һ�����ֱ任������һ��������ȷ���ģ��������������һ���ڵ��`node.next`��ȷ���ġ������������Ϳ������Ϊ��һ���������Ƿ���ڻ�����������ڻ������һ��Ԫ����1���ο���Ŀ[141. ��������](https://github.com/ustcyyw/yyw_algorithm/blob/master/easy/LinkedList/hasCycle.md)������������ʹ�ÿ���ָ���������
* ����һ��һ�������˶�Ա�������ֱ�����ܣ�������׷�����⣻������ڻ������ܣ��������һȦ����׷�����ġ�
* �����У��������ֱ�Ϊ1�������øñ任����õ��Ļ���1�������ж��Ƿ��ߵ�����βֻ��Ҫ�ж�`fast`�Ƿ�Ϊ1�����`fast == slow`����ָ���Ѿ�׷����ָ�룬�ɻ�����ָ��ÿ������������Ҳ�����������α任` fast = create(create(fast));`�����ѭ��������û�з��أ�˵��`fast == 1`����ʱ�ͷ���`true`��

���н����
* ִ����ʱ :1 ms, ������ Java �ύ�л�����99.89%���û�
* �ڴ����� :36.4 MB, ������ Java �ύ�л�����8.33%���û�

----
* ����LeetCode����뿴[���ֿ�](https://github.com/ustcyyw/yyw_algorithm)
* �������С�����Զ��������ο�[������Ŀ](https://github.com/ustcyyw/markdown_tool)
* [�ҵ�github](https://github.com/ustcyyw)���б��С��ĿҲ�ܺ��档��΢���~С����зз