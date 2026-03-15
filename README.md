# fagotto-brazil-updates

Actualizaciones y cambios fiscales requeridos para el módulo Brasil de Fagotto ERP — Reforma Tributaria 2026.

## Resumen

Este repositorio documenta las actualizaciones necesarias para el módulo **Brasil** de Fagotto ERP, en cumplimiento con la **Reforma Tributaria Brasileña 2026** (Lei Complementar 214/2025).

---

## Cambios Requeridos

### 1. Nuevos Impuestos: CBS e IBS

La reforma reemplaza los impuestos existentes (PIS, COFINS, ICMS, ISS, IPI) con un modelo dual de IVA:

| Impuesto | Ámbito | Reemplaza |
|----------|--------|-----------|
| **CBS** (Contribuição sobre Bens e Serviços) | Federal | PIS + COFINS |
| **IBS** (Imposto sobre Bens e Serviços) | Estadual/Municipal | ICMS + ISS |
| **IS** (Imposto Seletivo) | Federal | Aplicable a bienes específicos |

**Período de transición:** 2026–2033. Durante este período coexistirán el régimen antiguo y el nuevo.

- 2026: Tasas de prueba (sin impacto financiero real). Obligatoria la generación de los campos en NF-e/NFC-e.
- 2027: Inicio de la cobranza real de CBS/IBS.

### 2. Actualización de NF-e y NFC-e (Layout NT 2024.001)

A partir del **1 de enero de 2026**, los layouts de facturas electrónicas son obligatorios con nuevos campos:

- Campos para CBS, IBS e IS en el XML de NF-e/NFC-e.
- Nuevos esquemas XSD de validación.
- Nuevas reglas de validación en la SEFAZ.

**Acciones requeridas en Fagotto ERP:**
- [ ] Actualizar esquemas XML de NF-e (versión 4.00 actualizada).
- [ ] Actualizar esquemas XML de NFC-e.
- [ ] Implementar cálculo de CBS (alícuota inicial 0,9% en 2026).
- [ ] Implementar cálculo de IBS (alícuota inicial combinada estadual/municipal).
- [ ] Implementar cálculo de IS para bienes sujetos (bebidas, cigarrillos, vehículos, etc.).
- [ ] Actualizar certificación en ambiente de homologação (SEFAZ).

### 3. Nuevo Formato de CNPJ Alfanumérico

A partir de **julio de 2026**, el CNPJ adoptará un formato alfanumérico:

- Formato actual: 14 dígitos numéricos (XX.XXX.XXX/XXXX-DD).
- Nuevo formato: 14 caracteres alfanuméricos con nuevo algoritmo de dígito verificador.
- Ambos formatos coexistirán durante el período de transición.

**Acciones requeridas en Fagotto ERP:**
- [ ] Actualizar validación de CNPJ para aceptar caracteres alfanuméricos.
- [ ] Implementar nuevo algoritmo de cálculo del dígito verificador.
- [ ] Actualizar máscaras de entrada en formularios.
- [ ] Actualizar validaciones en importación de datos.

### 4. Split Payment (Pagamento Separado de Impostos)

El modelo de Split Payment implica la separación automática de los impuestos (CBS/IBS) en el momento del pago, remitiendo el valor directamente al fisco.

**Acciones requeridas en Fagotto ERP:**
- [ ] Implementar lógica de separación automática de CBS/IBS en el procesamiento de pagos.
- [ ] Actualizar módulo de cuentas por cobrar para reflejar el neto tras la retención.
- [ ] Generar asientos contables automáticos para la separación tributaria.
- [ ] Integrar con plataformas de pago que soporten Split Payment.

### 5. Validación en Tiempo Real

La SEFAZ implementará validación en tiempo real de los impuestos calculados:

- Si el impuesto calculado no coincide con el determinado por la autoridad fiscal, el documento pasa a estado **"Error"** y no puede ser autorizado.

**Acciones requeridas en Fagotto ERP:**
- [ ] Integrar con la API de validación de la SEFAZ.
- [ ] Implementar gestión del estado "Error" en documentos fiscales.
- [ ] Implementar flujo de corrección y reenvío de documentos con error.

---

## Cronograma

| Fecha | Hito |
|-------|------|
| 1 enero 2026 | NF-e/NFC-e con campos CBS/IBS/IS obligatorios (tasas de prueba) |
| Julio 2026 | CNPJ alfanumérico activo |
| 2027 | Cobranza real de CBS e IBS |
| 2029–2033 | Eliminación gradual del régimen antiguo |

---

## Referencias

- [Reforma Tributária - Receita Federal do Brasil](https://www.gov.br/receitafederal/pt-br/assuntos/legislacao/atos-normativos/instrucoes-normativas)
- [NT 2024.001 - NF-e/NFC-e Layout](https://www.nfe.fazenda.gov.br/portal/listaConteudo.aspx?tipoConteudo=Mn8Lc4+9gKQ=)
- [Lei Complementar 214/2025](https://www.planalto.gov.br/ccivil_03/leis/lcp/Lcp214.htm)
- [Resolução CNPJ Alfanumérico - Receita Federal](https://www.gov.br/receitafederal/pt-br)

