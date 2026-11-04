# one release for CLI tryout only

> **決議日期**:2026-11-04
> **來源**:[`../meeting-notes/YYYY-MM-DD-<topic>.md`](../meeting-notes/) / `requirements/tasks/TASK-xxx-*.md` / GitHub issue #NN / commit `<sha>`
> **動到的模組**:[`../spec/asgard/<module>.md`](../spec/asgard/)(可多個)

這是一份 dated 決議快照:記錄某個時間點「定了什麼、為什麼」。它不可變,
之後改變主意就寫新的一份,不要改這一份。當下唯一的行為在
[`../spec/asgard/`](../spec/asgard/)。

文字寫法見 [`.agents/skills/plain-chinese/`](../../.agents/skills/plain-chinese/)。
這份文件會被讀好幾年。像「為後續發展奠定基礎」這種句子,半年後有人翻出來想知道
到底定了什麼時,提供不了任何資訊。

## Summary

這個 repo 是為了試用 Asgard FDE CLI 建的,`.asgard-pipeline.yaml` 只宣告一條 release `tryout`,綁到既有的 `Tutorial` platform project。

## 決議

- **改了什麼**:`.asgard-pipeline.yaml` 的 `releases` 從雙 release(dev + prod)預設改成單條 `tryout`,觸發 pattern `^v[0-9]+\.[0-9]+\.[0-9]+$`。
- **為什麼**:這份 repo 是一次性的 CLI 試用,不會上線、不會有維運。brief 的 `../.agents/skills/asgard-platform/guide/projects.md` 明說單 release 只在「沒人要維護的 POC」時才對。若之後要加 staging,就得把 Tutorial project、namespace、release 名都換掉。
- **誰拍板**:使用者在 CLI onboarding 選了「1 個 release(POC / 試用)」。

## 後果

- 無法在同一 namespace 同時跑 dev 與 prod;要加環境得另外開 platform project 與 release。
- `asgard-cli verify` 只對一條 release 檢查;雙環境的交叉錯誤(如用到了同一個 project)看不到。
- 無需人工步驟。

## 套用到 living spec 的 delta

- [ ] `docs/spec/asgard/<module>.md` § <段落> —— <改動摘要>
- [ ] `docs/spec/asgard/README.md` —— 更新模組索引 / 追溯表

## Tracking

- 任務規格:`requirements/tasks/TASK-xxx-*.md`
- commit / PR:

## Open Questions

- 還沒收斂、留待下次的問題。
