# CHANGELOG — Graph-Ready v1 → v1.1 (2026-08-10)

## Corrections to v1 (defects found in audit)
1. **Direction reversals** fixed against the relationship dictionary:
   - G_E025 now DeepSeek → High-Flyer (SPUN_OUT_FROM = new lab → origin)
   - G_E027 now Zhipu → Tsinghua, G_E028 now Moonshot → Tsinghua (ACADEMIC_SPINOUT_FROM = lab → university)
   - G_E037 now Google Brain → Alphabet, G_E038 now Meta FAIR → Meta Platforms (SUBSIDIARY_OF = division → parent)
2. **Person rows repaired** (G_N024–G_N030): a missing column had shifted inclusion_class/confidence/source_ids;
   rows realigned to the 16-field header. Country filled as professional base where blank.
3. **G_E029 retargeted**: Llama OPEN_SOURCE_INFLUENCE now Meta FAIR → DeepSeek (concrete recipient),
   evidence downgraded to "reported"; previously pointed at OpenAI with abstract-ecosystem description.

## Additions (August 2026 gap-filling research pass)
- **36 new nodes** (G_N031–G_N066): 16 people (Hinton, Shazeer, Schulman, Suleyman, Kai-Fu Lee, Alexandr Wang,
  Yang Zhilin, Leike, Wang Xiaochuan, Jiang Daxin, Yan Junjie, Tang Jie, Mensch, Lample, Lacroix, Zoph),
  Chinese parents (Alibaba, ByteDance, Baidu, Tencent, SenseTime) + Tongyi Lab and ByteDance Seed,
  capital/compute (Amazon, Google Cloud, SoftBank), acqui-hire targets (Inflection, Character.AI, Scale AI),
  Mistral AI, Sinovation, Sogou, MSRA, DNNresearch, CMU, Meta Superintelligence Labs.
- **79 new edges** (G_E039–G_E117), including 5 new DERIVED founder-lineage edges (Sogou→Baichuan,
  MSRA→StepFun, SenseTime→MiniMax, FAIR→Mistral, DeepMind→Mistral), each carrying primitive edge IDs
  and a derivation rule.
- **40 new sources** (S015–S054) and **10 new uncertainty items** (U011–U020).
- Previously isolated nodes de-isolated: MiniMax, Baichuan, 01.AI, StepFun, NVIDIA. Baidu remains
  deliberately edge-less pending lab-level documentation (U016).

## Vocabulary decisions made during merge (review before freeze)
- Research edge "Tang Jie ADVISED Yang Zhilin" (person→person) violated ADVISED (person→lab);
  converted to ADVISED_BY (Yang → Tang, student→advisor), evidence "reported" (U013).
- Yang Zhilin's CMU advisors (Salakhutdinov, Cohen) folded into the STUDIED_AT edge note rather
  than creating advisor person-nodes.
- Microsoft–Inflection and Google–Character.AI encoded as ACQUIRED with explicit
  "acqui-hire-without-acquisition" caveat notes (U014). Consider minting an ACQUIHIRE type.
- Pre-Alphabet "Google" actions (DNNresearch 2013, Google China 2005–09) mapped to the Alphabet
  node with notes, matching v1's handling.
- Research duplicates of already-corrected v1 edges (Zhipu/Moonshot spinouts, Llama retarget)
  were not double-added.
- Four SUBSIDIARY_OF edges added from parent_node fields (Tongyi→Alibaba, Seed→ByteDance,
  MSL→Meta, MSRA→Microsoft, Google Cloud→Alphabet) per the v1 audit rule that parent
  relationships become edges, not attributes.

## Integrity checks passed
No dangling edge references; all derived edges carry primitives; 66 nodes / 117 edges /
53 sources / 20 uncertainty rows.

## v1.2 (2026-08-11) - Mirror Grid data migration
- Seven-channel expansion: PEOPLE, METHODS, MODELS, MONEY, MACHINES + DATA + EVALUATION.
- 27 new nodes (G_N067-G_N093): 12 Mirror Grid model nodes with seven mg_* attribute columns, 6 corpus nodes, 6 benchmark nodes, Huawei, Prosperity7 Ventures, Kingdom Holding.
- 75 new edges (G_E118-G_E192): MODEL_OF; TRAINED_ON_CORPUS (documented vs reported shared-pool, U021); ALLEGED_DISTILLATION (evidence=alleged, U022); EVALUATED_ON; chip/cloud granularity (Huawei Ascend->Zhipu, NVIDIA A100->DeepSeek, TPU->GDM, Alibaba/Tencent cloud U023); Saudi cross-border capital (Prosperity7->Zhipu, Kingdom Holding->xAI).
- New vocabulary: entity_type model/corpus/benchmark; relationship_type MODEL_OF, TRAINED_ON_CORPUS, ALLEGED_DISTILLATION, EVALUATED_ON; evidence_level "alleged".
- Mirror pairings deliberately NOT encoded as edges; similarity is computable from mg_* attributes.
- Interpretive content of the Mirror Grid (Dodd/Wormser, POSIWID, neutral-party) deliberately excluded from the dataset.
- Sources S055-S065; uncertainty U021-U025.

## v1.2.1 (2026-08-11) - verification pass, first tranche
- ALLEGED_DISTILLATION scope corrected: Anthropic's 2026-02-23 disclosure names THREE labs; added G_E193 Claude->DeepSeek (~150k exchanges) and G_E194 ChatGPT->DeepSeek (OpenAI open-letter allegation, separate accuser). All remain evidence=alleged, now with primary accuser sourcing.
- Huawei->Zhipu UPGRADED: primary Zhipu announcement (GLM-Image end-to-end on Ascend, 2026-01-14).
- KHC->xAI UPGRADED: Tadawul filing, $400M Series B + $400M Series C = $800M.
- Prosperity7->Zhipu corrected: date 2023->2024-05; DOWNGRADED confirmed->strongly supported (FT-sourced, unannounced).
- NVIDIA A100->DeepSeek enriched: Fire-Flyer II, ~10k A100s, completed 2021, Liang 2023 interview.
- Remaining for research run: Alibaba/Tencent cloud-hosting primary confirmation, evaluation-landscape audit + channel verdicts, Section 17 chronology, post-March inheritance sweep.

## v1.2.1 audit fixes (2026-08-11)
- AUDIT FINDING: v1.2.1 verification patch had written Huawei/Fire-Flyer text onto G_E185/G_E186 (TPU and Alibaba-cloud edges) instead of G_E183/G_E184. Descriptions and sources reassigned correctly; topology was never wrong.
- Header label corrected: 'Graph-Ready v1.2.1 - seven channels' (was stale v1.1 cosmetic text).
- Root cause of live-site discrepancy: repo still contains the v1.1 upload; v1.2/v1.2.1 zips were delivered but never uploaded to GitHub.

## v1.3 (2026-08-11) - Paradigm view
- Spec frozen (paradigm-departure-detector v1.0-FROZEN); 12x4 coding pass executed post-freeze from primary/technical documentation; data/paradigm.csv added (codings, deltas, evidence tiers, d_paradigm).
- New 'Paradigm' tab: HAS ANYONE MOVED? matrix. Result: 9 CONVENTIONAL, 1 HYBRID (Qwen 3.5, documented 3:1 Gated DeltaNet linear/full attention), 1 SUBSTRATE-DIVERGENT (GLM-5, Ascend, paradigm unchanged), 1 INSUFFICIENT (Copilot/MAI, R unknown). A1 entropy now 0.414 bits - no longer a constant column. T/R/E remain constant across known values. MiniMax 01->M2.5 recorded as documented temporary departure + reconvergence.
