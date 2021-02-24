# ゴール設定

## Lack of Knowledge

```mermaid
flowchart LR
    A[[Lack of Knowledges]] --> B(Engineering)
    A --> C(General)

    B --> B1(RDBMSの理論設計)
    B --> B2(DevOpsの概念やトレンド)
    B --> B3(クラウドネイティブな設計理論)
    B --> B4(AWS環境下での非機能設計)
    B --> B5(Front Knowledge)
    subgraph lack
        B1
        B2 --> B21(冪等生)
        B3 --> B31(密結合理解)
        B3 --> B32(疎結合理解)
        B4 --> B41("性能 (レイテンシ/スループット)")
        B5 --> B51(HTML/CSS)
        B5 --> B52("JavaScript (React/Vue)")
    end

    C --> C1(英語)
    C --> C2(統計知識)
    C --> C3(資産形成)
    subgraph lack
        C1 --> C11(中学英文法)
        C1 --> C12(長文読解)
        C1 --> C13(リスニング)
        C1 --> C14(スピーキング)
        C2 --> C21(統計検定2級相当)
        C3 --> C31(インデックス)
        C3 --> C32(ETF)
        C3 --> C33(節税)
        C3 --> C34(副業)
    end
```

[![](https://mermaid.ink/img/eyJjb2RlIjoiZmxvd2NoYXJ0IExSXG4gICAgQVtbTGFjayBvZiBLbm93bGVkZ2VzXV0gLS0-IEIoRW5naW5lZXJpbmcpXG4gICAgQSAtLT4gQyhHZW5lcmFsKVxuXG4gICAgQiAtLT4gQjEoUkRCTVPjga7nkIboq5boqK3oqIgpXG4gICAgQiAtLT4gQjIoRGV2T3Bz44Gu5qaC5b-144KE44OI44Os44Oz44OJKVxuICAgIEIgLS0-IEIzKOOCr-ODqeOCpuODieODjeOCpOODhuOCo-ODluOBquioreioiOeQhuirlilcbiAgICBCIC0tPiBCNChBV1PnkrDlooPkuIvjgafjga7pnZ7mqZ_og73oqK3oqIgpXG4gICAgQiAtLT4gQjUoRnJvbnQgS25vd2xlZGdlKVxuICAgIHN1YmdyYXBoIGxhY2tcbiAgICAgICAgQjFcbiAgICAgICAgQjIgLS0-IEIyMSjlhqrnrYnnlJ8pXG4gICAgICAgIEIzIC0tPiBCMzEo5a-G57WQ5ZCI55CG6KejKVxuICAgICAgICBCMyAtLT4gQjMyKOeWjue1kOWQiOeQhuinoylcbiAgICAgICAgQjQgLS0-IEI0MShcIuaAp-iDvSAo44Os44Kk44OG44Oz44K3L-OCueODq-ODvOODl-ODg-ODiClcIilcbiAgICAgICAgQjUgLS0-IEI1MShIVE1ML0NTUylcbiAgICAgICAgQjUgLS0-IEI1MihcIkphdmFTY3JpcHQgKFJlYWN0L1Z1ZSlcIilcbiAgICBlbmRcblxuICAgIEMgLS0-IEMxKOiLseiqnilcbiAgICBDIC0tPiBDMijntbHoqIjnn6XorZgpXG4gICAgQyAtLT4gQzMo6LOH55Sj5b2i5oiQKVxuICAgIHN1YmdyYXBoIGxhY2tcbiAgICAgICAgQzEgLS0-IEMxMSjkuK3lraboi7Hmlofms5UpXG4gICAgICAgIEMxIC0tPiBDMTIo6ZW35paH6Kqt6KejKVxuICAgICAgICBDMSAtLT4gQzEzKOODquOCueODi-ODs-OCsClcbiAgICAgICAgQzEgLS0-IEMxNCjjgrnjg5Tjg7zjgq3jg7PjgrApXG4gICAgICAgIEMyIC0tPiBDMjEo57Wx6KiI5qSc5a6aMue0muebuOW9kylcbiAgICAgICAgQzMgLS0-IEMzMSjjgqTjg7Pjg4fjg4Pjgq_jgrkpXG4gICAgICAgIEMzIC0tPiBDMzIoRVRGKVxuICAgICAgICBDMyAtLT4gQzMzKOevgOeojilcbiAgICAgICAgQzMgLS0-IEMzNCjlia_mpa0pXG4gICAgZW5kIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZmxvd2NoYXJ0IExSXG4gICAgQVtbTGFjayBvZiBLbm93bGVkZ2VzXV0gLS0-IEIoRW5naW5lZXJpbmcpXG4gICAgQSAtLT4gQyhHZW5lcmFsKVxuXG4gICAgQiAtLT4gQjEoUkRCTVPjga7nkIboq5boqK3oqIgpXG4gICAgQiAtLT4gQjIoRGV2T3Bz44Gu5qaC5b-144KE44OI44Os44Oz44OJKVxuICAgIEIgLS0-IEIzKOOCr-ODqeOCpuODieODjeOCpOODhuOCo-ODluOBquioreioiOeQhuirlilcbiAgICBCIC0tPiBCNChBV1PnkrDlooPkuIvjgafjga7pnZ7mqZ_og73oqK3oqIgpXG4gICAgQiAtLT4gQjUoRnJvbnQgS25vd2xlZGdlKVxuICAgIHN1YmdyYXBoIGxhY2tcbiAgICAgICAgQjFcbiAgICAgICAgQjIgLS0-IEIyMSjlhqrnrYnnlJ8pXG4gICAgICAgIEIzIC0tPiBCMzEo5a-G57WQ5ZCI55CG6KejKVxuICAgICAgICBCMyAtLT4gQjMyKOeWjue1kOWQiOeQhuinoylcbiAgICAgICAgQjQgLS0-IEI0MShcIuaAp-iDvSAo44Os44Kk44OG44Oz44K3L-OCueODq-ODvOODl-ODg-ODiClcIilcbiAgICAgICAgQjUgLS0-IEI1MShIVE1ML0NTUylcbiAgICAgICAgQjUgLS0-IEI1MihcIkphdmFTY3JpcHQgKFJlYWN0L1Z1ZSlcIilcbiAgICBlbmRcblxuICAgIEMgLS0-IEMxKOiLseiqnilcbiAgICBDIC0tPiBDMijntbHoqIjnn6XorZgpXG4gICAgQyAtLT4gQzMo6LOH55Sj5b2i5oiQKVxuICAgIHN1YmdyYXBoIGxhY2tcbiAgICAgICAgQzEgLS0-IEMxMSjkuK3lraboi7Hmlofms5UpXG4gICAgICAgIEMxIC0tPiBDMTIo6ZW35paH6Kqt6KejKVxuICAgICAgICBDMSAtLT4gQzEzKOODquOCueODi-ODs-OCsClcbiAgICAgICAgQzEgLS0-IEMxNCjjgrnjg5Tjg7zjgq3jg7PjgrApXG4gICAgICAgIEMyIC0tPiBDMjEo57Wx6KiI5qSc5a6aMue0muebuOW9kylcbiAgICAgICAgQzMgLS0-IEMzMSjjgqTjg7Pjg4fjg4Pjgq_jgrkpXG4gICAgICAgIEMzIC0tPiBDMzIoRVRGKVxuICAgICAgICBDMyAtLT4gQzMzKOevgOeojilcbiAgICAgICAgQzMgLS0-IEMzNCjlia_mpa0pXG4gICAgZW5kIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)