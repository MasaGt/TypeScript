### アクセス修飾子

- TypeScriptでは、Javaと同じようなアクセス修飾子を使うことができる

---

### 種類

- なし: publicと同じ

- public: どこからでもアクセスできる

- protected: 自身のクラスとサブクラスからのみアクセス可能

- private: 自身のクラスのみアクセス可能

```Typescript
class Animal {
  public name: string;
 
  public constructor(theName: string) {
    this.name = theName;
  }
 
  // 自身か、サブクラスからのみアクセス可能
  protected move() {
    // 処理内容
  }

  // 自身からのみアクセス可能
  private roar() {
    // 処理内容 
  }

}

```