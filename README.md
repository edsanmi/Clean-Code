# **Clean Code em TypeScript**

**Clean Code** (Código Limpo) é um conjunto de práticas e princípios que ajudam a escrever código mais **legível, manutenível e eficiente**. O conceito foi popularizado pelo livro *"Clean Code: A Handbook of Agile Software Craftsmanship"*, de **Robert C. Martin (Uncle Bob)**.

---

## **Princípios Fundamentais do Clean Code**

1. **Nomes significativos**
2. **Funções pequenas e de responsabilidade única**
3. **Evitar código duplicado**
4. **Comentários úteis (mas só quando necessário)**
5. **Tratamento de erros adequado**
6. **Código simples e direto**
7. **Evitar dependências desnecessárias**
8. **Formatação consistente**

---

## **1. Nomes significativos**

### **Problema: Nomes vagos e confusos**
```typescript
function calc(a: number, b: number): number {
    return a * b;
}
```

### **Solução: Nomes descritivos e claros**
```typescript
function calculateTotalPrice(quantity: number, pricePerUnit: number): number {
    return quantity * pricePerUnit;
}
```

**Boas práticas:**
- Use **nomes descritivos**, evitando abreviações excessivas.
- Nomeie variáveis e funções de acordo com sua **intenção**.
- Evite nomes genéricos como `data`, `temp`, `info`.

---

## **2. Funções pequenas e de responsabilidade única (SRP)**

### **Problema: Funções longas e complexas**
```typescript
function processOrder(order: any) {
    console.log("Validating order...");
    if (!order.isValid) {
        throw new Error("Invalid order");
    }

    console.log("Processing payment...");
    // lógica de pagamento...

    console.log("Sending email confirmation...");
    // lógica de envio de e-mail...
}
```

### **Solução: Dividir em funções menores e mais coesas**
```typescript
function validateOrder(order: any): void {
    if (!order.isValid) {
        throw new Error("Invalid order");
    }
}

function processPayment(order: any): void {
    console.log("Processing payment...");
    // lógica de pagamento...
}

function sendConfirmationEmail(order: any): void {
    console.log("Sending email confirmation...");
    // lógica de envio de e-mail...
}

function processOrder(order: any): void {
    validateOrder(order);
    processPayment(order);
    sendConfirmationEmail(order);
}
```

**Boas práticas:**
- Cada função deve fazer **apenas uma coisa**.
- Funções pequenas são mais **fáceis de entender e reutilizar**.

---

## **3. Evitar código duplicado (DRY - Don't Repeat Yourself)**

### **Problema: Código duplicado em várias partes do sistema**
```typescript
function calculateDiscountedPrice(price: number, discount: number): number {
    return price - (price * discount) / 100;
}

function applyDiscountToProduct(price: number, discount: number): number {
    return price - (price * discount) / 100;
}
```

### **Solução: Criar uma função reutilizável**
```typescript
function applyDiscount(price: number, discount: number): number {
    return price - (price * discount) / 100;
}
```

**Boas práticas:**
- Extraia lógica repetitiva em funções reutilizáveis.
- Use **abstrações** para evitar duplicação.

---

## **4. Comentários úteis (mas só quando necessário)**

### **Problema: Comentários desnecessários explicando o óbvio**
```typescript
// Verifica se o usuário está autenticado
if (user.isAuthenticated) {
    // Redireciona para a página inicial
    redirectToHome();
}
```

### **Solução: Código autoexplicativo**
```typescript
if (user.isAuthenticated) {
    redirectToHome();
}
```

**Boas práticas:**
- Prefira **código autoexplicativo** em vez de comentários desnecessários.
- Use comentários **apenas** para contexto adicional ou explicações complexas.

---

## **5. Tratamento de erros adequado**

### **Problema: Ignorar ou tratar erros de forma genérica**
```typescript
try {
    processPayment();
} catch (error) {
    console.log("Erro ao processar pagamento");
}
```

### **Solução: Tratar erros de forma específica e clara**
```typescript
try {
    processPayment();
} catch (error) {
    console.error("Falha ao processar pagamento:", error.message);
    sendAlertToAdmin(error);
}
```

**Boas práticas:**
- Trate **erros específicos**, fornecendo mensagens úteis.
- Evite capturar erros silenciosamente sem registro.

---

## **6. Código simples e direto**

### **Problema: Lógica desnecessariamente complexa**
```typescript
function isAdult(age: number): boolean {
    if (age >= 18) {
        return true;
    } else {
        return false;
    }
}
```

### **Solução: Código direto e conciso**
```typescript
function isAdult(age: number): boolean {
    return age >= 18;
}
```

**Boas práticas:**
- Elimine código redundante.
- Prefira **simplicidade sobre complexidade**.

---

## **7. Evitar dependências desnecessárias**

### **Problema: Importar bibliotecas desnecessárias**
```typescript
import _ from 'lodash';

function isEmptyString(str: string): boolean {
    return _.isEmpty(str);
}
```

### **Solução: Usar recursos nativos do TypeScript**
```typescript
function isEmptyString(str: string): boolean {
    return str.trim() === '';
}
```

**Boas práticas:**
- Avalie se realmente precisa de uma **biblioteca externa**.
- Evite dependências que podem ser resolvidas com código nativo.

---

## **8. Formatação consistente**

### **Problema: Formatação inconsistente do código**
```typescript
function soma (a:number, b:number) {return a+b;}
```

### **Solução: Formatação padronizada com Prettier**
```typescript
function soma(a: number, b: number): number {
    return a + b;
}
```

**Boas práticas:**
- Use ferramentas como **Prettier** ou **ESLint** para manter a formatação consistente.
- Siga as convenções da equipe/projeto.

---

## **Resumo de Práticas Clean Code**

| Princípio                  | Resumo                                   |
|----------------------------|------------------------------------------|
| **Nomes significativos**    | Use nomes claros e descritivos.          |
| **Funções pequenas**        | Uma função deve fazer apenas uma coisa.  |
| **Evitar duplicação (DRY)** | Centralize lógica comum em funções.      |
| **Comentários úteis**       | Somente quando necessário.               |
| **Tratamento de erros**     | Forneça mensagens claras e específicas.  |
| **Código simples**          | Evite complexidade desnecessária.        |
| **Evitar dependências**     | Prefira soluções nativas sempre que possível. |
| **Formatação consistente**  | Use ferramentas para padronização.       |

---

## **Ferramentas para ajudar a manter Clean Code em TypeScript**

1. **ESLint** - Analisador de código para identificar e corrigir problemas de estilo.
2. **Prettier** - Ferramenta para formatar código automaticamente.
3. **TypeScript** - Utilizar tipagem para melhorar clareza e evitar erros.
4. **Jest/Mocha** - Testes unitários para validar regras de negócio.

---

Essas práticas de **Clean Code** tornam o código mais **manutenível**, **colaborativo** e **menos propenso a erros**.

Se precisar de mais exemplos ou explicações, estou à disposição!
