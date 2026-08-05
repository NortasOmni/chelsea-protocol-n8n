# Состояние 10 пунктов и реестр затронутых workflow — Chelsea v10

Основа: `Chelsea_Hardening_staged_2026-08-04_v10_point_5_complete.zip`. Сравнение существующих workflow выполнено с пакетом `Chelsea_Hardening_staged_2026-08-03.zip`.

## Итог по файлам

- Актуальных staged-workflow: **112**.
- Изменено существовавших workflow с сохранённым ID: **16**.
- Новый модульный State Scheduler заменяет старый Scheduler v4.3: **1**.
- Остальных новых workflow: **95**.
- Все 112 staged-workflow находятся в `99_all_current_staged_workflows_112`.

## Состояние пунктов

| № | Статус | Что остаётся | Прямо затронуто workflow |
|---:|---|---|---:|
| 1 | ✅ Staged-код завершён | Production SQL/bootstrap/migration/cutover не выполнены. | 26 |
| 2 | ✅ Staged-код завершён | Реальные ключи не ротированы; ENV/Credentials production не настроены. | 52 |
| 3 | ✅ Staged-код завершён | Live red-team на фактических OpenAI/KIE моделях не выполнен. | 17 |
| 4 | 🟡 Технически подготовлено | SQL не применён, backfill и concurrency/crash tests на реальной PostgreSQL не выполнены. | 10 |
| 5 | ✅ Staged-код завершён | Shadow/cutover на реальных задачах и измерение latency не выполнены. | 66 |
| 6 | 🔴 Не завершён | Importer не создаёт/не remap-ит Data Tables; Dependency Health содержит несовместимые поля/имена. | 8 |
| 7 | 🟡 Частично | Error Handler и Reliability Monitor имеют остаточные дефекты подтверждения Telegram alerts. | 11 |
| 8 | 🟡 Частично | Нет live export→delivery→delete; есть ENV naming mismatch и зависимость от неприменённого SQL/Data Tables. | 15 |
| 9 | ✅ Завершён в пакете | Production-архивы на сервере не проверены. | 12 |
| 10 | 🟡 Частично | Нет real import/PostgreSQL/Telegram/Qdrant/privacy E2E; тесты не ловят часть известных дефектов. | 7 |

## Пункт 1

**Статус:** ✅ Staged-код завершён

**Как затронул:** Перевод identity на numeric Telegram actor ID, PostgreSQL authority, actor-only storage namespaces, legacy bootstrap/migration и downstream identity boundary.

**Ограничение:** Production SQL/bootstrap/migration/cutover не выполнены.

Затронутых workflow в реестре: **26**.

- `Chelsea Identity Authority v2.0 — HARDENED STAGED` — `IdAuthV1x7Nq4Kb` — новый workflow.
- `Chelsea Identity Batch Migration v1.0 — HARDENED STAGED` — `IdBatchV198b1d7e8` — новый workflow.
- `Chelsea Identity Data Table Migration Target v1.0 — HARDENED STAGED` — `IdMigTblV1x9Q2aB` — новый workflow.
- `Chelsea Identity Legacy Bootstrap and Readiness v2.0 — HARDENED STAGED` — `IdAuditV1m8Hs3Qa` — новый workflow.
- `Chelsea Immutable Identity Migration v2.0 — HARDENED STAGED` — `IdMigMainV1p7Z4cD` — новый workflow.
- `Chelsea Privacy Consent Intake v1.0 — HARDENED STAGED` — `CNS4mT8qL2vR7pXa` — новый workflow.
- `Chelsea Privacy Request Intake v1.0 — HARDENED STAGED` — `kq7AsKLn7RX1Viv7` — новый workflow.
- `Chelsea Privacy Telegram Router v1.0 — HARDENED STAGED` — `PRIVRTR7b2c3d4e5f6a` — новый workflow.
- `Chelsea Resolution Questions v3.0 [HARDENED STAGED]` — `JdJJcYvZdJgJiElS` — изменён существовавший workflow.
- `Chelsea Task Intent Shadow v1.0 — HARDENED STAGED` — `JPpslgT3mncJzEEy` — новый workflow.
- `Chelsea Task Operation Normalize Trusted Task Input v1.0 — HARDENED STAGED` — `T1025d0ce7ad99f4` — новый workflow.
- `Chelsea Task Operation Prepare Registered Task Users v1.0 — HARDENED STAGED` — `T104273c7aa49eee` — новый workflow.
- `Chelsea Task Operation Verify Folder User Identity v1.0 — HARDENED STAGED` — `T100abdfea74ba71` — новый workflow.
- `Process Chelsea State QdrantOutbox Worker v1.0 — HARDENED STAGED` — `puNfqcIG1OEjLpPU` — новый workflow.
- `Qdrant загрузка и контроль знаний v6.1 — HARDENED STAGED` — `QRD9aL2xK7mP4vNs` — новый workflow.
- `Создать папки пользователя v4.0 — HARDENED STAGED` — `FLD8wK3pR6tY2qHb` — новый workflow.
- `Челси identity resolver v4.0 — HARDENED STAGED` — `kX2iJZ0Bm3hhTjwX` — изменён существовавший workflow.
- `Челси ТГ бот Obsidian v9.0 [HARDENED STAGED]` — `j0oV9b3T0CCLKMxL` — изменён существовавший workflow.
- `Челси ТГ входная схема v9.0 [HARDENED STAGED]` — `5GAzkL7PzohlOycF` — изменён существовавший workflow.
- `Челси диспетчер уточнений v3.1 [HARDENED STAGED]` — `COC56dbrXhYqRgFP` — изменён существовавший workflow.
- `Челси задачи команды v2.0 [HARDENED STAGED]` — `iG8uV66FHyyQZyn8` — изменён существовавший workflow.
- `Челси задачи планировщик v2.1 [HARDENED STAGED]` — `7VsagxmTKlmJ1YJ8` — изменён существовавший workflow.
- `Челси обработчик очереди памяти v2.9 replacement [HARDENED STAGED]` — `N3GFoezvVmoj0wyp` — изменён существовавший workflow.
- `Челси очередь памяти enqueue v2.3 [HARDENED STAGED]` — `tWHSD8lBIbiHA3D5` — изменён существовавший workflow.
- `Челси применение уточнений v3.0 [HARDENED STAGED]` — `by3HcLFOyOHMZa6H` — изменён существовавший workflow.
- `Челси регистрация пользователя v3.0 — HARDENED STAGED` — `Q5JF6Ora2lIjKVeV` — изменён существовавший workflow.

## Пункт 2

**Статус:** ✅ Staged-код завершён

**Как затронул:** Удаление секретов из item-flow, перевод HTTP auth на ENV/Credentials, отключение сохранения execution payload и redaction ошибок.

**Ограничение:** Реальные ключи не ротированы; ENV/Credentials production не настроены.

Настройки сохранения execution data изменены у **всех 112** workflow. Ниже перечислены **52 workflow**, которые дополнительно непосредственно используют ENV или n8n Credentials.

Затронутых workflow в реестре: **52**.

- `Chelsea Consent Gate v1.0 — HARDENED STAGED` — `CONSENT7A2b3c4d5e6f` — новый workflow.
- `Chelsea Critical Store Backfill v1.0 — HARDENED STAGED` — `BFL4mN8qR2vT7pXa` — новый workflow.
- `Chelsea DLQ Inspector v1.0 — HARDENED STAGED` — `XTYsdwtfZk2RBbBn` — новый workflow.
- `Chelsea Dependency Health Check v1.0 — HARDENED STAGED` — `DJmQO3G2NwsP9Cbf` — новый workflow.
- `Chelsea Deployment Preflight v1.0 — HARDENED STAGED` — `PFL5cN7vR2mX8qWa` — новый workflow.
- `Chelsea Error Handler v1.0 — HARDENED STAGED` — `gSoMnSr3MCWcU7Ox` — новый workflow.
- `Chelsea Identity Authority v2.0 — HARDENED STAGED` — `IdAuthV1x7Nq4Kb` — новый workflow.
- `Chelsea Identity Batch Migration v1.0 — HARDENED STAGED` — `IdBatchV198b1d7e8` — новый workflow.
- `Chelsea Identity Legacy Bootstrap and Readiness v2.0 — HARDENED STAGED` — `IdAuditV1m8Hs3Qa` — новый workflow.
- `Chelsea Immutable Identity Migration v2.0 — HARDENED STAGED` — `IdMigMainV1p7Z4cD` — новый workflow.
- `Chelsea Integration Smoke Tests v1.0 — HARDENED STAGED` — `rY0nkke3WnwcTnf7` — новый workflow.
- `Chelsea Privacy Artifact Cleanup Worker v1.0 — HARDENED STAGED` — `PRIVCLN7d4e5f6a7b8c` — новый workflow.
- `Chelsea Privacy Consent Intake v1.0 — HARDENED STAGED` — `CNS4mT8qL2vR7pXa` — новый workflow.
- `Chelsea Privacy Export Delivery v1.0 — HARDENED STAGED` — `PRIVDLV7b523f9511cf4` — новый workflow.
- `Chelsea Privacy Outbox Worker v1.0 — HARDENED STAGED` — `zYOv6rLZVEjAiTNf` — новый workflow.
- `Chelsea Privacy Request Intake v1.0 — HARDENED STAGED` — `kq7AsKLn7RX1Viv7` — новый workflow.
- `Chelsea Privacy Telegram Router v1.0 — HARDENED STAGED` — `PRIVRTR7b2c3d4e5f6a` — новый workflow.
- `Chelsea Qdrant Privacy Adapter v1.0 — HARDENED STAGED` — `QDP8nT5cL2vR7mXa` — новый workflow.
- `Chelsea Reliability Monitor v1.0 — HARDENED STAGED` — `RELMON7c3d4e5f6a7b` — новый workflow.
- `Chelsea Resolution Questions v3.0 [HARDENED STAGED]` — `JdJJcYvZdJgJiElS` — изменён существовавший workflow.
- `Chelsea Scheduler Lease Guard v1.0 — HARDENED STAGED` — `FiTw7NHWsbSqg6RP` — новый workflow.
- `Chelsea Scheduler Orchestrator v1.0 — HARDENED STAGED` — `SCH7nM4xV2cL9pQa` — новый workflow.
- `Process Chelsea State Analysis Worker v1.0 — HARDENED STAGED` — `1uZ5KCubNPTyKuh5` — новый workflow.
- `Process Chelsea State ChangeNotification Worker v1.0 — HARDENED STAGED` — `jMZYEOqeUpKg19oD` — новый workflow.
- `Process Chelsea State ClarificationAnswer Worker v1.0 — HARDENED STAGED` — `bE5XAWq7GWHdwZbU` — новый workflow.
- `Process Chelsea State ClarificationAsk Worker v1.0 — HARDENED STAGED` — `AnAStMDvOcgg9QQj` — новый workflow.
- `Process Chelsea State ClarificationFinalize Worker v1.0 — HARDENED STAGED` — `4Wi9cqjk2Mz7CSXq` — новый workflow.
- `Process Chelsea State Decision Worker v1.0 — HARDENED STAGED` — `OY9mgITJVR4nHuT9` — новый workflow.
- `Process Chelsea State Delivery Worker v1.0 — HARDENED STAGED` — `VFcTLbdfS3Ec838w` — новый workflow.
- `Process Chelsea State Evaluation Worker v1.0 — HARDENED STAGED` — `cVYLgM5y9YyBkRxZ` — новый workflow.
- `Process Chelsea State FuturePlanFollowUp Worker v1.0 — HARDENED STAGED` — `qgWN2jDgXChDsbbe` — новый workflow.
- `Process Chelsea State InteractionRecovery Worker v1.0 — HARDENED STAGED` — `lairbKhoaq0o05aA` — новый workflow.
- `Process Chelsea State Operations Worker v1.0 — HARDENED STAGED` — `04ODyCDlNaIRgTuU` — новый workflow.
- `Process Chelsea State Proactivity Worker v1.0 — HARDENED STAGED` — `cX6ay5aMXH3wdL0v` — новый workflow.
- `Process Chelsea State QdrantOutbox Worker v1.0 — HARDENED STAGED` — `puNfqcIG1OEjLpPU` — новый workflow.
- `Process Chelsea State StateDateRoute Worker v1.0 — HARDENED STAGED` — `q6omiaG4yYgYcwVl` — новый workflow.
- `Process | Chelsea State | Core v2.0 [HARDENED STAGED]` — `tIraOM8RkQAc2pvw` — изменён существовавший workflow.
- `Qdrant загрузка и контроль знаний v6.1 — HARDENED STAGED` — `QRD9aL2xK7mP4vNs` — новый workflow.
- `Создать папки пользователя v4.0 — HARDENED STAGED` — `FLD8wK3pR6tY2qHb` — новый workflow.
- `Стандартные вопросы Челси v3.0 [HARDENED STAGED]` — `3T5zBQvkyu3mW9xe` — изменён существовавший workflow.
- `Челси ТГ бот Obsidian v9.0 [HARDENED STAGED]` — `j0oV9b3T0CCLKMxL` — изменён существовавший workflow.
- `Челси ТГ входная схема v9.0 [HARDENED STAGED]` — `5GAzkL7PzohlOycF` — изменён существовавший workflow.
- `Челси быстрая реакция worker v2.1 [HARDENED STAGED]` — `EWzVuvIxi7Ee8TEu` — изменён существовавший workflow.
- `Челси диспетчер уточнений v3.1 [HARDENED STAGED]` — `COC56dbrXhYqRgFP` — изменён существовавший workflow.
- `Челси доставка взаимодействий v1.0 [HARDENED STAGED]` — `awa3pS7rw4fCNEVt` — изменён существовавший workflow.
- `Челси задачи команды v2.0 [HARDENED STAGED]` — `iG8uV66FHyyQZyn8` — изменён существовавший workflow.
- `Челси задачи планировщик v2.1 [HARDENED STAGED]` — `7VsagxmTKlmJ1YJ8` — изменён существовавший workflow.
- `Челси запуск взаимодействия v2.0 [HARDENED STAGED]` — `T05mXj4RA2mfvMoB` — изменён существовавший workflow.
- `Челси обработчик очереди памяти v2.9 replacement [HARDENED STAGED]` — `N3GFoezvVmoj0wyp` — изменён существовавший workflow.
- `Челси очередь памяти enqueue v2.3 [HARDENED STAGED]` — `tWHSD8lBIbiHA3D5` — изменён существовавший workflow.
- `Челси применение уточнений v3.0 [HARDENED STAGED]` — `by3HcLFOyOHMZa6H` — изменён существовавший workflow.
- `Челси регистрация пользователя v3.0 — HARDENED STAGED` — `Q5JF6Ora2lIjKVeV` — изменён существовавший workflow.

## Пункт 3

**Статус:** ✅ Staged-код завершён

**Как затронул:** Обязательные pre-LLM/post-LLM gateways, output validator и memory candidate validator для всех генеративных вызовов.

**Ограничение:** Live red-team на фактических OpenAI/KIE моделях не выполнен.

Затронутых workflow в реестре: **17**.

- `Chelsea LLM Raw Response Security Gateway v3.0 — HARDENED STAGED` — `LLMRawSecV1e9PaT` — новый workflow.
- `Chelsea LLM Request Security Gateway v3.0 — HARDENED STAGED` — `LLMReqSecV1d2WxY` — новый workflow.
- `Chelsea Memory Candidate Security Validator v3.0 — HARDENED STAGED` — `MemorySecV1c4TuV` — новый workflow.
- `Chelsea Model Output Security Validator v3.0 — HARDENED STAGED` — `ModelOutSecV1b6QrS` — новый workflow.
- `Chelsea Prompt Security Gateway v3.0 — HARDENED STAGED` — `PromptSecGwV1a8LmN` — новый workflow.
- `Process Chelsea State Analysis Worker v1.0 — HARDENED STAGED` — `1uZ5KCubNPTyKuh5` — новый workflow.
- `Process Chelsea State ClarificationAnswer Worker v1.0 — HARDENED STAGED` — `bE5XAWq7GWHdwZbU` — новый workflow.
- `Process Chelsea State ClarificationAsk Worker v1.0 — HARDENED STAGED` — `AnAStMDvOcgg9QQj` — новый workflow.
- `Process Chelsea State ClarificationFinalize Worker v1.0 — HARDENED STAGED` — `4Wi9cqjk2Mz7CSXq` — новый workflow.
- `Process Chelsea State Proactivity Worker v1.0 — HARDENED STAGED` — `cX6ay5aMXH3wdL0v` — новый workflow.
- `Process Chelsea State StateDateRoute Worker v1.0 — HARDENED STAGED` — `q6omiaG4yYgYcwVl` — новый workflow.
- `Стандартные вопросы Челси v3.0 [HARDENED STAGED]` — `3T5zBQvkyu3mW9xe` — изменён существовавший workflow.
- `Челси ТГ бот Obsidian v9.0 [HARDENED STAGED]` — `j0oV9b3T0CCLKMxL` — изменён существовавший workflow.
- `Челси ТГ входная схема v9.0 [HARDENED STAGED]` — `5GAzkL7PzohlOycF` — изменён существовавший workflow.
- `Челси быстрая реакция worker v2.1 [HARDENED STAGED]` — `EWzVuvIxi7Ee8TEu` — изменён существовавший workflow.
- `Челси задачи команды v2.0 [HARDENED STAGED]` — `iG8uV66FHyyQZyn8` — изменён существовавший workflow.
- `Челси применение уточнений v3.0 [HARDENED STAGED]` — `by3HcLFOyOHMZa6H` — изменён существовавший workflow.

## Пункт 4

**Статус:** 🟡 Технически подготовлено

**Как затронул:** Перенос критических очередей tasks/memory/resolution/response jobs на PostgreSQL record store, CAS и atomic claim RPC.

**Ограничение:** SQL не применён, backfill и concurrency/crash tests на реальной PostgreSQL не выполнены.

Затронутых workflow в реестре: **10**.

- `Chelsea Critical Store Backfill v1.0 — HARDENED STAGED` — `BFL4mN8qR2vT7pXa` — новый workflow.
- `Chelsea Resolution Questions v3.0 [HARDENED STAGED]` — `JdJJcYvZdJgJiElS` — изменён существовавший workflow.
- `Челси ТГ бот Obsidian v9.0 [HARDENED STAGED]` — `j0oV9b3T0CCLKMxL` — изменён существовавший workflow.
- `Челси ТГ входная схема v9.0 [HARDENED STAGED]` — `5GAzkL7PzohlOycF` — изменён существовавший workflow.
- `Челси диспетчер уточнений v3.1 [HARDENED STAGED]` — `COC56dbrXhYqRgFP` — изменён существовавший workflow.
- `Челси задачи команды v2.0 [HARDENED STAGED]` — `iG8uV66FHyyQZyn8` — изменён существовавший workflow.
- `Челси задачи планировщик v2.1 [HARDENED STAGED]` — `7VsagxmTKlmJ1YJ8` — изменён существовавший workflow.
- `Челси обработчик очереди памяти v2.9 replacement [HARDENED STAGED]` — `N3GFoezvVmoj0wyp` — изменён существовавший workflow.
- `Челси очередь памяти enqueue v2.3 [HARDENED STAGED]` — `tWHSD8lBIbiHA3D5` — изменён существовавший workflow.
- `Челси применение уточнений v3.0 [HARDENED STAGED]` — `by3HcLFOyOHMZa6H` — изменён существовавший workflow.

## Пункт 5

**Статус:** ✅ Staged-код завершён

**Как затронул:** Разделение Task Domain и State Scheduler на тонкие маршрутизаторы, 22 operation workflow, mutation branches и 14 State workers.

**Ограничение:** Shadow/cutover на реальных задачах и измерение latency не выполнены.

Затронутых workflow в реестре: **66**.

- `Chelsea Task Answer Branch Cancel Draft v1.0 — HARDENED STAGED` — `TM10812fc805a729a` — новый workflow.
- `Chelsea Task Answer Branch Create Draft Needs Details v1.0 — HARDENED STAGED` — `TM1051e0681770416` — новый workflow.
- `Chelsea Task Answer Branch Mutation Draft v1.0 — HARDENED STAGED` — `TM107206b8fcafd66` — новый workflow.
- `Chelsea Task Answer Branch Needs Details v1.0 — HARDENED STAGED` — `TM1062776ad6c450a` — новый workflow.
- `Chelsea Task Answer Branch Normal v1.0 — HARDENED STAGED` — `TM10c432016f8c4a7` — новый workflow.
- `Chelsea Task Answer Branch Terminal v1.0 — HARDENED STAGED` — `TM10c9f19bbed9e51` — новый workflow.
- `Chelsea Task Domain Runtime v2.0 — MODULAR HARDENED STAGED` — `M4JqA5dzW7rC9sTx` — новый workflow.
- `Chelsea Task Mutation Branch Create Draft Answer v1.0 — HARDENED STAGED` — `TM10b0febcc818c0c` — новый workflow.
- `Chelsea Task Mutation Branch Pre Route v1.0 — HARDENED STAGED` — `TM105b5cd21f3fecc` — новый workflow.
- `Chelsea Task Mutation Branch Task Answer v1.0 — HARDENED STAGED` — `TM102b6ad5e40f252` — новый workflow.
- `Chelsea Task Operation Attach Telegram Key to Task Action v1.0 — HARDENED STAGED` — `T10d0678e94dee69` — новый workflow.
- `Chelsea Task Operation Build Telegram Task Response v1.0 — HARDENED STAGED` — `T10bc4d97a3476f3` — новый workflow.
- `Chelsea Task Operation Finalize Telegram Task Delivery v1.0 — HARDENED STAGED` — `T10af49d550a9600` — новый workflow.
- `Chelsea Task Operation Finalize Telegram Task Receipt v1.0 — HARDENED STAGED` — `T101bde66b6cf26c` — новый workflow.
- `Chelsea Task Operation Finalize Verified Task Command Saga v1.0 — HARDENED STAGED` — `T10cccd671a11087` — новый workflow.
- `Chelsea Task Operation Normalize Trusted Task Input v1.0 — HARDENED STAGED` — `T1025d0ce7ad99f4` — новый workflow.
- `Chelsea Task Operation Plan Expired Dispatch Reconciliation v1.0 — HARDENED STAGED` — `T1055ec59562a258` — новый workflow.
- `Chelsea Task Operation Plan Internal Task Action v1.0 — HARDENED STAGED` — `T105888095b63685` — новый workflow.
- `Chelsea Task Operation Plan Task Action Claim v1.0 — HARDENED STAGED` — `T106c655bd8e065e` — новый workflow.
- `Chelsea Task Operation Plan Trusted Task Mutation v1.0 — HARDENED STAGED` — `T1014db58b06e187` — новый workflow.
- `Chelsea Task Operation Prepare Registered Task Users v1.0 — HARDENED STAGED` — `T104273c7aa49eee` — новый workflow.
- `Chelsea Task Operation Route Task Operation v1.0 — HARDENED STAGED` — `T102df83f961ee96` — новый workflow.
- `Chelsea Task Operation Select Due Task Actions v1.0 — HARDENED STAGED` — `T10d70c24a8dcf74` — новый workflow.
- `Chelsea Task Operation Verify Claim and Plan Action v1.0 — HARDENED STAGED` — `T10eff9a6c763ba3` — новый workflow.
- `Chelsea Task Operation Verify Dispatch and Build Telegram Action v1.0 — HARDENED STAGED` — `T108a9b93fc0d15d` — новый workflow.
- `Chelsea Task Operation Verify Expired Dispatch Reconciliation v1.0 — HARDENED STAGED` — `T10836409ec04587` — новый workflow.
- `Chelsea Task Operation Verify Folder User Identity v1.0 — HARDENED STAGED` — `T100abdfea74ba71` — новый workflow.
- `Chelsea Task Operation Verify Internal Task Mutation v1.0 — HARDENED STAGED` — `T10c3515f29855db` — новый workflow.
- `Chelsea Task Operation Verify Task Command Saga Mutation v1.0 — HARDENED STAGED` — `T1049d966a366c6a` — новый workflow.
- `Chelsea Task Operation Verify Task Delivery Mutation v1.0 — HARDENED STAGED` — `T1011cf85aa441ba` — новый workflow.
- `Chelsea Task Operation Verify Task Mutation Read Back v1.0 — HARDENED STAGED` — `T103471a71f8c2ca` — новый workflow.
- `Chelsea Task Operation Verify Task Question Receipt v1.0 — HARDENED STAGED` — `T10111afa8d29e81` — новый workflow.
- `Chelsea Task Resume Branch Already Active v1.0 — HARDENED STAGED` — `TM10cec23d5534890` — новый workflow.
- `Chelsea Task Resume Branch Direct v1.0 — HARDENED STAGED` — `TM10e68b25d803c8b` — новый workflow.
- `Chelsea Task Resume Branch Interrupted v1.0 — HARDENED STAGED` — `TM101c19853253419` — новый workflow.
- `Chelsea Task Resume Branch Saga v1.0 — HARDENED STAGED` — `TM10ccbadad402fbc` — новый workflow.
- `Chelsea Task Resume Branch Terminal v1.0 — HARDENED STAGED` — `TM10474f43359d19a` — новый workflow.
- `Chelsea Task Semantic Branch Cancel Series v1.0 — HARDENED STAGED` — `TM1000359ac234037` — новый workflow.
- `Chelsea Task Semantic Branch Clarification v1.0 — HARDENED STAGED` — `TM10dc11af9a683cf` — новый workflow.
- `Chelsea Task Semantic Branch Create Series v1.0 — HARDENED STAGED` — `TM109b672786c183a` — новый workflow.
- `Chelsea Task Semantic Branch Create v1.0 — HARDENED STAGED` — `TM109923a89e2320a` — новый workflow.
- `Chelsea Task Semantic Branch Direct Mutation v1.0 — HARDENED STAGED` — `TM10f5a134c98a4cf` — новый workflow.
- `Chelsea Task Semantic Branch Outcome v1.0 — HARDENED STAGED` — `TM104c3b1b81f45d5` — новый workflow.
- `Chelsea Task Semantic Branch Resume Series v1.0 — HARDENED STAGED` — `TM10d624728b9541f` — новый workflow.
- `Chelsea Task Semantic Branch Terminal v1.0 — HARDENED STAGED` — `TM10576b8acf8d316` — новый workflow.
- `Chelsea Task Semantic Mutation Router v1.0 — HARDENED STAGED` — `TMSem1021924750f` — новый workflow.
- `Process Chelsea State Analysis Parser v1.0 — HARDENED STAGED` — `STPARSE6xA1b2c3d4` — новый workflow.
- `Process Chelsea State Analysis Request Builder v1.0 — HARDENED STAGED` — `StateReqBuild083e` — новый workflow.
- `Process Chelsea State Analysis Worker v1.0 — HARDENED STAGED` — `1uZ5KCubNPTyKuh5` — новый workflow.
- `Process Chelsea State ChangeNotification Worker v1.0 — HARDENED STAGED` — `jMZYEOqeUpKg19oD` — новый workflow.
- `Process Chelsea State ClarificationAnswer Worker v1.0 — HARDENED STAGED` — `bE5XAWq7GWHdwZbU` — новый workflow.
- `Process Chelsea State ClarificationAsk Worker v1.0 — HARDENED STAGED` — `AnAStMDvOcgg9QQj` — новый workflow.
- `Process Chelsea State ClarificationFinalize Worker v1.0 — HARDENED STAGED` — `4Wi9cqjk2Mz7CSXq` — новый workflow.
- `Process Chelsea State Decision Worker v1.0 — HARDENED STAGED` — `OY9mgITJVR4nHuT9` — новый workflow.
- `Process Chelsea State Delivery Worker v1.0 — HARDENED STAGED` — `VFcTLbdfS3Ec838w` — новый workflow.
- `Process Chelsea State Evaluation Worker v1.0 — HARDENED STAGED` — `cVYLgM5y9YyBkRxZ` — новый workflow.
- `Process Chelsea State FuturePlanFollowUp Worker v1.0 — HARDENED STAGED` — `qgWN2jDgXChDsbbe` — новый workflow.
- `Process Chelsea State InteractionRecovery Worker v1.0 — HARDENED STAGED` — `lairbKhoaq0o05aA` — новый workflow.
- `Process Chelsea State Operations Worker v1.0 — HARDENED STAGED` — `04ODyCDlNaIRgTuU` — новый workflow.
- `Process Chelsea State Proactivity Worker v1.0 — HARDENED STAGED` — `cX6ay5aMXH3wdL0v` — новый workflow.
- `Process Chelsea State QdrantOutbox Worker v1.0 — HARDENED STAGED` — `puNfqcIG1OEjLpPU` — новый workflow.
- `Process Chelsea State Scheduler v5.0 — MODULAR HARDENED STAGED` — `STF6pQ2mN9xR4vKa` — новый workflow; заменяет старый Scheduler v4.3 (ID XfKJbLpfQOGdXd3M).
- `Process Chelsea State StateDateRoute Worker v1.0 — HARDENED STAGED` — `q6omiaG4yYgYcwVl` — новый workflow.
- `Process | Chelsea State | Core v2.0 [HARDENED STAGED]` — `tIraOM8RkQAc2pvw` — изменён существовавший workflow.
- `Челси задачи команды v2.0 [HARDENED STAGED]` — `iG8uV66FHyyQZyn8` — изменён существовавший workflow.
- `Челси задачи планировщик v2.1 [HARDENED STAGED]` — `7VsagxmTKlmJ1YJ8` — изменён существовавший workflow.

## Пункт 6

**Статус:** 🔴 Не завершён

**Как затронул:** Добавление недостающих Qdrant/folder dependencies, health/preflight/smoke wiring и проверка внутренней Execute Workflow связности.

**Ограничение:** Importer не создаёт/не remap-ит Data Tables; Dependency Health содержит несовместимые поля/имена.

Затронутых workflow в реестре: **8**.

- `Chelsea Dependency Health Check v1.0 — HARDENED STAGED` — `DJmQO3G2NwsP9Cbf` — новый workflow.
- `Chelsea Deployment Preflight v1.0 — HARDENED STAGED` — `PFL5cN7vR2mX8qWa` — новый workflow.
- `Chelsea Integration Smoke Tests v1.0 — HARDENED STAGED` — `rY0nkke3WnwcTnf7` — новый workflow.
- `Chelsea Task Operation Verify Folder User Identity v1.0 — HARDENED STAGED` — `T100abdfea74ba71` — новый workflow.
- `Qdrant загрузка и контроль знаний v6.1 — HARDENED STAGED` — `QRD9aL2xK7mP4vNs` — новый workflow.
- `Создать папки пользователя v4.0 — HARDENED STAGED` — `FLD8wK3pR6tY2qHb` — новый workflow.
- `Челси identity resolver v4.0 — HARDENED STAGED` — `kX2iJZ0Bm3hhTjwX` — изменён существовавший workflow.
- `Челси регистрация пользователя v3.0 — HARDENED STAGED` — `Q5JF6Ora2lIjKVeV` — изменён существовавший workflow.

## Пункт 7

**Статус:** 🟡 Частично

**Как затронул:** Timeouts, fenced leases, scheduler orchestration, retry/backoff/DLQ, error events и operator monitoring.

**Ограничение:** Error Handler и Reliability Monitor имеют остаточные дефекты подтверждения Telegram alerts.

Затронутых workflow в реестре: **11**.

- `Chelsea DLQ Inspector v1.0 — HARDENED STAGED` — `XTYsdwtfZk2RBbBn` — новый workflow.
- `Chelsea Error Handler v1.0 — HARDENED STAGED` — `gSoMnSr3MCWcU7Ox` — новый workflow.
- `Chelsea Privacy Artifact Cleanup Worker v1.0 — HARDENED STAGED` — `PRIVCLN7d4e5f6a7b8c` — новый workflow.
- `Chelsea Privacy Outbox Worker v1.0 — HARDENED STAGED` — `zYOv6rLZVEjAiTNf` — новый workflow.
- `Chelsea Reliability Monitor v1.0 — HARDENED STAGED` — `RELMON7c3d4e5f6a7b` — новый workflow.
- `Chelsea Scheduler Lease Guard v1.0 — HARDENED STAGED` — `FiTw7NHWsbSqg6RP` — новый workflow.
- `Chelsea Scheduler Orchestrator v1.0 — HARDENED STAGED` — `SCH7nM4xV2cL9pQa` — новый workflow.
- `Process Chelsea State Scheduler v5.0 — MODULAR HARDENED STAGED` — `STF6pQ2mN9xR4vKa` — новый workflow; заменяет старый Scheduler v4.3 (ID XfKJbLpfQOGdXd3M).
- `Челси диспетчер уточнений v3.1 [HARDENED STAGED]` — `COC56dbrXhYqRgFP` — изменён существовавший workflow.
- `Челси задачи планировщик v2.1 [HARDENED STAGED]` — `7VsagxmTKlmJ1YJ8` — изменён существовавший workflow.
- `Челси обработчик очереди памяти v2.9 replacement [HARDENED STAGED]` — `N3GFoezvVmoj0wyp` — изменён существовавший workflow.

## Пункт 8

**Статус:** 🟡 Частично

**Как затронул:** Privacy export/status/delete/consent через Telegram, outbox, adapters, bundle delivery, TTL cleanup и consent gates.

**Ограничение:** Нет live export→delivery→delete; есть ENV naming mismatch и зависимость от неприменённого SQL/Data Tables.

Затронутых workflow в реестре: **15**.

- `Chelsea Consent Gate v1.0 — HARDENED STAGED` — `CONSENT7A2b3c4d5e6f` — новый workflow.
- `Chelsea Files Privacy Adapter v1.0 — HARDENED STAGED` — `FPR5xC9mN2qL7vBd` — новый workflow.
- `Chelsea Legacy Data Tables Privacy Adapter v1.0 — HARDENED STAGED` — `DTP7mR4xK2qV9sLc` — новый workflow.
- `Chelsea Privacy Artifact Cleanup Worker v1.0 — HARDENED STAGED` — `PRIVCLN7d4e5f6a7b8c` — новый workflow.
- `Chelsea Privacy Consent Intake v1.0 — HARDENED STAGED` — `CNS4mT8qL2vR7pXa` — новый workflow.
- `Chelsea Privacy Export Delivery v1.0 — HARDENED STAGED` — `PRIVDLV7b523f9511cf4` — новый workflow.
- `Chelsea Privacy Outbox Worker v1.0 — HARDENED STAGED` — `zYOv6rLZVEjAiTNf` — новый workflow.
- `Chelsea Privacy Request Intake v1.0 — HARDENED STAGED` — `kq7AsKLn7RX1Viv7` — новый workflow.
- `Chelsea Privacy Telegram Router v1.0 — HARDENED STAGED` — `PRIVRTR7b2c3d4e5f6a` — новый workflow.
- `Chelsea Qdrant Privacy Adapter v1.0 — HARDENED STAGED` — `QDP8nT5cL2vR7mXa` — новый workflow.
- `Chelsea Scheduler Orchestrator v1.0 — HARDENED STAGED` — `SCH7nM4xV2cL9pQa` — новый workflow.
- `Process Chelsea State Proactivity Worker v1.0 — HARDENED STAGED` — `cX6ay5aMXH3wdL0v` — новый workflow.
- `Process | Chelsea State | Core v2.0 [HARDENED STAGED]` — `tIraOM8RkQAc2pvw` — изменён существовавший workflow.
- `Челси ТГ входная схема v9.0 [HARDENED STAGED]` — `5GAzkL7PzohlOycF` — изменён существовавший workflow.
- `Челси очередь памяти enqueue v2.3 [HARDENED STAGED]` — `tWHSD8lBIbiHA3D5` — изменён существовавший workflow.

## Пункт 9

**Статус:** ✅ Завершён в пакете

**Как затронул:** Sanitized archive и rollback copies: inactive, без credentials и без автоматических triggers; исключены из importer.

**Ограничение:** Production-архивы на сервере не проверены.

Затронуты 6 sanitized archive JSON и 6 rollback JSON. Полный список находится в папке `09_point_9` и CSV-реестре.

## Пункт 10

**Статус:** 🟡 Частично

**Как затронул:** Smoke/preflight/shadow/backfill/readiness workflow и статические/контрактные тесты; live E2E пока отсутствует.

**Ограничение:** Нет real import/PostgreSQL/Telegram/Qdrant/privacy E2E; тесты не ловят часть известных дефектов.

Затронутых workflow в реестре: **7**.

- `Chelsea Critical Store Backfill v1.0 — HARDENED STAGED` — `BFL4mN8qR2vT7pXa` — новый workflow.
- `Chelsea Dependency Health Check v1.0 — HARDENED STAGED` — `DJmQO3G2NwsP9Cbf` — новый workflow.
- `Chelsea Deployment Preflight v1.0 — HARDENED STAGED` — `PFL5cN7vR2mX8qWa` — новый workflow.
- `Chelsea Identity Legacy Bootstrap and Readiness v2.0 — HARDENED STAGED` — `IdAuditV1m8Hs3Qa` — новый workflow.
- `Chelsea Integration Smoke Tests v1.0 — HARDENED STAGED` — `rY0nkke3WnwcTnf7` — новый workflow.
- `Chelsea State Intake Shadow v1.0 — HARDENED STAGED` — `zW9Ny2Is64j3nO8e` — новый workflow.
- `Chelsea Task Intent Shadow v1.0 — HARDENED STAGED` — `JPpslgT3mncJzEEy` — новый workflow.

## Важные замечания

- Один workflow может относиться сразу к нескольким пунктам. Поэтому файлы в папках пунктов могут дублироваться.
- Папка `99_all_current_staged_workflows_112` — полный актуальный импортируемый staged-набор.
- Папка `98_changed_existing_workflows_16` содержит workflow, которые существовали в базовом пакете и были изменены с сохранением ID.
- Папка `97_new_workflows_96` содержит новые workflow, включая новый State Scheduler.
- Production не изменён: это staged JSON, а не подтверждение фактического импорта/активации.
