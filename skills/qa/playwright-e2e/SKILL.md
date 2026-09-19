---
name: playwright-e2e
description: >-
  Especialista em testes ponta a ponta (E2E) com Microsoft Playwright.
  Aplica abordagem mobile-first (360px a 430px), Page Object Model (POM),
  reutilização de estado de autenticação (storageState) e locators acessíveis e resilientes.
---

# 🎭 Playwright E2E Testing Standards

Esta skill padroniza a criação de testes End-to-End automatizados para garantir que os fluxos críticos de negócio nunca quebrem em produção.

---

## 📱 Princípios Mobile-First & Confiabilidade

1. **Viewports Móveis Obrigatórias**: Toda suite de testes deve rodar primariamente em viewports móveis (ex: `iPhone 14` / `390x844` ou `Pixel 7` / `412x915`), além do desktop (`1280x720`).
2. **Locators Acessíveis (User-Centric)**:
   - ✅ **Preferir**: `page.getByRole('button', { name: 'Salvar' })`, `page.getByLabel('Data do Plantão')`, `page.getByTestId('shift-card')`.
   - ❌ **Evitar**: Seletores CSS frágeis como `.btn.primary > div:nth-child(2) > span`.
3. **Zero `page.waitForTimeout()` arbitrário**: Esperas cegas (`sleep(3000)`) geram testes lentos e instáveis (*flaky*). Use sempre assertions com auto-wait: `await expect(page.getByText('Plantão salvo com sucesso')).toBeVisible()`.
4. **Reutilização de Autenticação (`storageState`)**: Não faça login interativo via UI em cada teste. Realize o login uma única vez no setup global e reutilize a sessão autenticada.

---

## 🏛️ Padrão Page Object Model (POM)

```typescript
// tests/e2e/pages/shift-page.ts
import { Page, Locator, expect } from '@playwright/test';

export class ShiftPage {
  readonly page: Page;
  readonly newShiftButton: Locator;
  readonly hospitalInput: Locator;
  readonly amountInput: Locator;
  readonly saveButton: Locator;
  readonly successToast: Locator;

  constructor(page: Page) {
    this.page = page;
    this.newShiftButton = page.getByRole('button', { name: /novo plantão/i });
    this.hospitalInput = page.getByLabel(/hospital ou local/i);
    this.amountInput = page.getByLabel(/valor/i);
    this.saveButton = page.getByRole('button', { name: /salvar plantão/i });
    this.successToast = page.getByText(/plantão cadastrado com sucesso/i);
  }

  async goto() {
    await this.page.goto('/dashboard/plantoes');
  }

  async createShift(hospital: string, amount: string) {
    await this.newShiftButton.click();
    await this.hospitalInput.fill(hospital);
    await this.amountInput.fill(amount);
    await this.saveButton.click();
  }

  async expectSuccess() {
    await expect(this.successToast).toBeVisible({ timeout: 5000 });
  }
}
```

---

## 🧪 Exemplo de Teste E2E

```typescript
// tests/e2e/shifts.spec.ts
import { test, expect } from '@playwright/test';
import { ShiftPage } from './pages/shift-page';

test.describe('Gestão de Plantões', () => {
  test('deve criar um novo plantão com saldo calculado corretamente', async ({ page }) => {
    const shiftPage = new ShiftPage(page);
    await shiftPage.goto();

    await shiftPage.createShift('Hospital Geral', '1500,00');
    await shiftPage.expectSuccess();

    // Valida que o card apareceu na lista com o valor correto
    const shiftCard = page.getByTestId('shift-card-Hospital Geral');
    await expect(shiftCard).toContainText('R$ 1.500,00');
    await expect(shiftCard).toContainText('Pendente');
  });
});
```

---

## ✅ Checklist de Qualidade do Teste

- [ ] O teste roda com sucesso tanto em viewport mobile quanto desktop?
- [ ] Nenhum seletor quebra se o layout CSS for ajustado?
- [ ] Não há `waitForTimeout` com tempo fixo no código?
- [ ] O teste limpa ou isola os dados criados (idempotência)?
- [ ] O teste passa de forma consistente sem falhas intermitentes (*flakiness*)?
