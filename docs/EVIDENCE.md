# Evidence registry

What Sidekick grades, suggests and rewards, and the research behind each rule. Nothing here is shown in the app; it
decides what the prompts, the skill anchors and the route lenses are allowed to say. The plan that produced it is
`PLAN-EVIDENCE.md`. Last full check: 2026-10-15.

## How to use it

**Tiers.** A: meta-analysis or replicated experiments. B: a single peer-reviewed study or a large field dataset.
C: vendor data (Gong and similar: large, correlational, self-interested). D: practitioner book. E: our own heuristic.

**The rule.** A behaviour may be *graded* (a 1-5 anchor line, a moment grade, a route lens line that says "is
Inquiry 4+") only with a tier A or B claim behind it. Tier C, D and E rules may appear as coaching: a lens sentence
that says "a good habit, not a score", a focus track, a drill, a card's wording. Never as a score or a penalty.

**Changing a rule.** Add or update the row below first, with a source someone else can open (DOI or publisher page;
never cite from memory). Then change the prompt or the route. `backend/tests/test_evidence.py` fails when a claim id
used in the prompts has no row here, or when a bundled route's achievement is missing from the route map.

**Upkeep.** Once a quarter: new meta-analyses in the clusters below; vendor refreshes go in at tier C only.

## Claims

| id | What Sidekick does now | Tier | Verdict | Key sources |
|---|---|---|---|---|
| C1 | Live card: silence by default; speak when an answer is due, the position changed, a wrong claim will cost, a commitment would evaporate, or a goal opening will pass | B | partly supported | Tanveer 2015; Ofek 2013 |
| C2 | Live card: hold while they talk themselves toward the USER's position | E | no direct evidence | (follows from C1) |
| C3 | Filler hedges, apologies, over-justifying, answering unasked questions are faults; calibrated uncertainty and one constraint reason are not | A | partly supported, context-dependent | Hosman 1989; Blankenship & Holtgraves 2005; Fragale 2006; Jensen 2008; Tenney 2007; Maaravi 2011; Lee & Ames 2017; Lee, Mason & Malcomb 2024 |
| C4 | Card line of 15 words shown about 150 ms after they stop; never while the USER talks | A | contradicted on readability (gaps ~200 ms, tolerance ~600 ms); open, see PLAN-EVIDENCE Phase 3 | Stivers 2009; Levinson & Torreira 2015; Roberts & Francis 2013; Templeton 2022 |
| C5 | Six dimensions: clarity, inquiry, influence, pushback, closing, composure | E | construct untested; validate by retranslation | Smith & Kendall 1963 (method) |
| C6 | Clarity: numbers, names and dates instead of adjectives; one question at a time | B | concreteness supported; compound questions survey-only | Packard & Berger 2021; Oppenheimer 2006; Larrimore 2011; Menold 2020 |
| C7 | Inquiry: follow-ups built on the last answer until a priority, number, owner or constraint is pinned | A | supported | Huang et al. 2017; Thompson 1991; Zerres 2013; Minson 2018 |
| C8 | Influence: a recommendation with its cost and what would change it; others reuse the USER's term or number | B | partly, by proxy | Brennan & Clark 1996; Taylor & Thomas 2008; Sniezek & Van Swol 2001; Tenney 2007 |
| C9 | Pushback: acknowledge the point, name the disagreement, give the fact or alternative; challenge alone costs the speaker | A | supported in this form | Yeomans et al. 2020; Burris 2012; Chamberlin 2017; Whiting 2012; Hüffmeier 2014 |
| C10 | Closing: every open item leaves with an owner and a date; the decision said back | A/B | supported in direction | Kauffeld & Lehmann-Willenbrock 2012; Gollwitzer & Sheeran 2006; Mroz 2018 |
| C11 | Composure: pause to think before a hard answer; take the floor when a view is due; hold back while others work | A/B | supported with conditions; silence creates value, it does not make them concede | Curhan 2022; MacLaren 2020; Mullen 1989; Woolley 2010 |
| C12 | Moment penalties and accuracy = 100 x (1 - sum / N) | E | unvalidated until the labelled set exists | (PLAN-GROWTH §4.5) |
| C13 | No grade for talking more or less; a held silence is good or great only when it let them think or improve their offer | B | supported as conditioned | MacLaren 2020; Curhan 2022 |
| C14 | Accepting their vague number is a mistake; a price or date not tied to an agreed scope is a mistake | A/B | supported (precision); indirect (sequencing) | Janiszewski & Uy 2008; Mason 2013; Loschelder 2016; Weingart 1993; Leonardelli 2019 |
| C15 | Open first with an ambitious, precise, defensible figure when informed; when they anchor, return to your own target | A | supported with conditions | Galinsky & Mussweiler 2001; Gunia 2013; Maaravi 2014; Maaravi & Levy 2017 |
| C16 | No concession without a condition or a trade; a concession that matches theirs is a trade | A | partly supported | Hüffmeier 2014; Esser & Komorita 1975; Kwon & Weingart 2004; Alavi 2016 |
| C17 | Sales: budget, decider and timeline come out during the call, not as an opening checklist | C/D | partly supported; habit only | Gong (budget study); Rackham 1988 |
| C18 | Sales: ask what the problem costs before the product; no long uninterrupted pitch | C/D | partly supported; habit only | Rackham 1988; Gong (demos) |
| C19 | Sales: the buyer commits to a dated next step; a seller-only promise is not an advance | C/D | supported in direction; graded only through C10 | Rackham 1988; Gong (next steps) |
| C20 | One-to-ones: the manager lets the other person do most of the talking; asks before advising | B | supported (survey evidence) | Rogelberg 2024; Rogelberg 2022 |
| C21 | Feedback names the behaviour and the example, about the work, never the person; softening is not a fault | A | supported | Kluger & DeNisi 1996; Hattie & Timperley 2007; Parkes 2013 |
| C22 | Chairing a group decision: the question and how it will be decided first, own view last; as an advisor, answer first | A | supported (previous rule contradicted) | Lu, Yuan & McLeod 2012; Larson 1998; Bonaccio & Dalal 2006 |
| C23 | Six or more at the table is a harder room | B | supported in direction | Hosseinkashi 2024; Karau & Williams 1993 |
| C24 | Interviews: structured questions and follow-ups; situational questions count; no selling the role | A | supported | Sackett 2022; Levashina 2014; Culbertson 2017; Marr & Cable 2014 |
| C25 | Status meetings: a proposed fix instead of a complaint joined; "one number first" and "what changed" are habits | B | complaining cycles supported; the two habits have no evidence | Kauffeld & Meyers 2009; Mroz 2018 |
| C26 | Escalations: apology, a short factual explanation, a fix with a date; no blame | A | supported | Gelbrich & Roschk 2011; Roschk & Kaiser 2013; Davidow 2003 |
| C27 | New scope named as a change, with its impact and a decision asked for | B | partly supported (survey) | Komal 2020 |
| C28 | Discovery: ask about past behaviour, today's workaround and the cost, not hypothetical liking | A | supported | Schmidt & Bijmolt 2020; Morwitz 2007 |
| C29 | Advising: lead with a costed recommendation and say what would change it | B | partly supported | Bonaccio & Dalal 2006; Sniezek & Van Swol 2001; Tenney 2007 |
| C30 | One goal per meeting that the USER controls, tied to a cue when one is foreseeable; side quests optional and easier | A | supported | Locke & Latham 2002; Gollwitzer & Sheeran 2006; Seijts & Latham 2005 |
| C31 | Review: quote-anchored moments with the stronger line; informational positives, never praise | A | supported | Kluger & DeNisi 1996; Finkelstein & Fishbach 2012; Deci, Koestner & Ryan 1999 |
| C32 | Drills with a spaced re-test | A | supported for retention | Roediger & Karpicke 2006; Dunlosky 2013; Cepeda 2008; Moore 2018 |
| C33 | Pattern broken after five relevant rounds | E | no evidence for five; see PLAN-EVIDENCE Phase 4 | Lally 2010; Wood & Neal 2007 |
| C34 | Levels with an uncertainty band; XP only rises; streaks; no leaderboards | B | supported as a model; calibrate before trusting trends | Pelánek 2016; Klinkenberg 2011; Sailer & Homner 2020; Silverman & Barasch 2023 |
| C35 | The judge's promotion gate | B | needs human labels and Krippendorff's alpha per skill | Zheng 2023; Ye 2025; Norman 2026 |
| C36 | What weighs most depends on the meeting kind (in the judge prompt, not in the rating math) | E | stated design; follows the claims above per kind | (PLAN-GROWTH §4.2) |
| C37 | Walk-away: reveal only a strong alternative; anchor on the target, not the reservation price | B | supported for strong alternatives | Pinkley 1994; Schaerer 2015; Buelens & Van Poucke 2004 |
| C38 | Never coach bluffing; share priorities, never the reservation price | A | supported | Kong, Dirks & Ferrin 2014; Van Zant 2022; Thompson 1991 |
| C39 | The full stronger line lives in the review and drills; live help stays short | B | supported | Tanveer 2015; Hohenstein 2023; Samrose 2020 |
| C40 | Softened phrasing in a second language is not graded as hedging | A/B | supported in direction | Circi 2021; Lev-Ari & Keysar 2010 |

## Route map

Every bundled route's achievements and the claims that back them. A route lens may grade only through these.

| route | achievements and claims |
|---|---|
| `sell-the-room` | `point_of_view` C8 C29 · `room_moved` C8 · `no_thoughts` C10 · `one_breath` C6 · `big_room_view` C8 C23 |
| `chair-the-decision` | `view_first` C22 · `room_changed_mind` C8 · `tested_it` C9 · `decision_owned` C10 · `big_table` C22 C23 |
| `close-the-deal` | `qualified` C7 · `held_the_price` C16 · `always_a_next_step` C10 · `problem_first` C8 C28 · `closed_it` C30 |
| `hold-the-number` | `the_number` C7 C14 · `traded` C16 · `cold_silence` C11 · `scope_first` C14 · `steady_hand` C12 |
| `run-the-account` | `clean_brief` C10 · `said_no_kindly` C9 C27 · `one_number` C6 · `asked_for_it` C8 C29 · `ten_for_ten` C30 |
| `run-the-ops` | `one_number_first` C6 · `what_changed` C7 · `no_orphan_blockers` C10 · `fix_it_properly` C9 C27 · `reliable` C10 |
| `hold-the-plan` | `traded_not_given` C16 C27 · `saw_it_coming` C6 · `decided_in_room` C10 · `held_the_date` C10 · `calm_under_change` C11 |
| `keep-the-customer` | `renewal_question` C7 · `owned_it` C26 · `both_ways` C10 · `their_words` C6 · `kept_every_promise` C10 |
| `ship-the-roadmap` | `found_the_problem` C7 C28 · `said_not_now` C9 · `evidence_won` C8 · `demo_asked_back` C10 · `shipped_on_time` C10 |
| `lead-the-team` | `listened_first` C7 C20 · `plain_feedback` C21 · `handed_it_over` C10 · `steady_hand` C11 · `kept_your_word` C10 |
| `hire-well` | `got_the_example` C24 · `held_the_silence` C11 · `clear_next_step` C10 · `fair_and_clear` C6 C24 · `twenty_in` C30 |

Achievement ids never change (they are stored in people's progress); names, descriptions and lenses may.
`steady_hand` in *Hold the number* counts accuracy, which is unvalidated (C12) until the labelled set exists.

## Sources (verified: publisher, DOI or Scholar record)

### Meeting science and organisational psychology
Kauffeld & Lehmann-Willenbrock 2012, Meetings matter, *Small Group Research* 43(2), 10.1177/1046496411429599 ·
Kauffeld & Meyers 2009, Complaint and solution-oriented circles, *EJWOP* 18, 10.1080/13594320701693209 ·
Mroz, Allen, Verhoeven & Shuffler 2018, Do we really need another meeting?, *Current Directions in Psychological Science*, 10.1177/0963721418776307 ·
Rogelberg 2024, *Glad We Met*, OUP (practitioner, survey evidence) · Rogelberg 2022, HBR, Make the most of your one-on-one meetings ·
Kluger & DeNisi 1996, *Psychological Bulletin* 119(2), 10.1037/0033-2909.119.2.254 · Hattie & Timperley 2007, *RER* 77(1), 10.3102/003465430298487 ·
Parkes, Abercrombie & McCarty 2013, *Adv. Health Sci. Educ.* 18(3), 10.1007/s10459-012-9377-9 · Prochazka, Ovcari & Durinik 2020, *Learning and Motivation* 71 ·
Goodman, Wood & Hendrickx 2004, *JAP* 89(2) · Larson, Foster-Fishman & Franz 1998, *PSPB* 24, 10.1177/0146167298245004 ·
Lu, Yuan & McLeod 2012, *Pers. Soc. Psych. Review* 16 · Edmondson 1999, *ASQ* 44(2) · Garvin & Roberto 2001, HBR (practitioner) ·
Sackett, Zhang, Berry & Lievens 2022, *JAP* 107(11) · Levashina, Hartwell, Morgeson & Campion 2014, *Personnel Psychology* 67, 10.1111/peps.12052 ·
Culbertson, Weyhrauch & Huffcutt 2017, *HRM Review* 27 · Marr & Cable 2014, *AMJ* 57 · Rowe 1986, *J. Teacher Education* 37(1) ·
Hosseinkashi, Tankelevitch, Pool, Cutler & Madan 2024, *PACM HCI* 8 CSCW1, 10.1145/3637370 · Karau & Williams 1993, *JPSP* 65(4) ·
Allen, Tong & Landowski 2020, *J. Management Development* 40(5), 10.1108/JMD-12-2019-0510 · Burris 2012, *AMJ* 55(4), 10.5465/amj.2010.0562 ·
Chamberlin, Newton & LePine 2017, *Personnel Psychology* 70, 10.1111/peps.12185 · Whiting, Maynes, Podsakoff & Podsakoff 2012, *JAP* 97(1) ·
Morrison 2014, *Annu. Rev. Org. Psych. Org. Behav.* 1, 10.1146/annurev-orgpsych-031413-091328 · Microsoft Work Trend Index 2023 (industry survey) ·
Corpora: AMI (groups.inf.ed.ac.uk/ami/corpus) · ICSI/MRDA · ELEA (Sanchez-Cortes, Aran & Gatica-Perez 2011) · MeetingBank (ACL 2023) · QMSum (NAACL 2021, arXiv:2104.05938)

### Negotiation
Hüffmeier, Freund, Zerres, Backhaus & Hertel 2014, *J. Management*, 10.1177/0149206311423788 · Esser & Komorita 1975, *JPSP*, 10.1037/h0076692 ·
Kwon & Weingart 2004, *JAP*, 10.1037/0021-9010.89.2.263 · Curhan, Overbeck, Cho, Zhang & Yang 2022, *JAP*, 10.1037/apl0000877 ·
Galinsky & Mussweiler 2001, *JPSP*, 10.1037/0022-3514.81.4.657 · Gunia, Swaab, Sivanathan & Galinsky 2013, *PSPB*, 10.1177/0146167213499236 ·
Guthrie & Orr 2006, *Ohio St. J. Disp. Resol.* 21 · Loschelder, Swaab, Trötschel & Galinsky 2014, *Psych. Science*, 10.1177/0956797613520168 ·
Maaravi & Levy 2017, *JDM*, 10.1017/s193029750000646x · Maaravi, Pazy & Ganzach 2014, *JDM*, 10.1017/S1930297500006410 ·
Janiszewski & Uy 2008, *Psych. Science*, 10.1111/j.1467-9280.2008.02057.x · Mason, Lee, Wiley & Ames 2013, *JESP*, 10.1016/j.jesp.2013.02.012 ·
Loschelder, Friese, Schaerer & Galinsky 2016, *Psych. Science*, 10.1177/0956797616666074 · Ames & Mason 2015, *JPSP*, 10.1037/pspi0000016 ·
Weingart, Bennett & Brett 1993, *JAP*, 10.1037/0021-9010.78.3.504 · Froman & Cohen 1970, *Behavioral Science*, 10.1002/bs.3830150209 ·
Leonardelli, Gu, McRuer, Medvec & Galinsky 2019, *OBHDP*, 10.1016/j.obhdp.2019.01.007 · Pinkley, Neale & Bennett 1994, *OBHDP*, 10.1006/obhd.1994.1006 ·
Pinkley 1995, *JAP*, 10.1037/0021-9010.80.3.403 · Schaerer, Swaab & Galinsky 2015, *Psych. Science*, 10.1177/0956797614558718 ·
Buelens & Van Poucke 2004, *J. Bus. Psychol.* · Thompson 1991, *JESP*, 10.1016/0022-1031(91)90020-7 · Zerres et al. 2013, *JAP*, 10.1037/a0032255 ·
Thompson & DeHarpport 1994, *OBHDP*, 10.1006/obhd.1994.1040 · Minson, VanEpps, Yip & Schweitzer 2018, *OBHDP*, 10.1016/j.obhdp.2018.05.006 ·
Maaravi, Ganzach & Pazy 2011, *JPSP*, 10.1037/a0023331 · Lee & Ames 2017, *OBHDP*, 10.1016/j.obhdp.2017.05.002 ·
Hyder, Prietula & Weingart 2000, *Cognitive Science*, 10.1016/s0364-0213(00)00021-5 · Lee, Mason & Malcomb 2024, *SPPS*, 10.1177/19485506241305486 ·
Kong, Dirks & Ferrin 2014, *AMJ*, 10.5465/amj.2012.0461 · Van Zant, Kennedy & Kray 2022, *JPSP*, 10.1037/pspi0000410 · Olekalns & Smith 2009, *J. Bus. Ethics* ·
Nadler, Thompson & Van Boven 2003, *Mgmt. Science*, 10.1287/mnsc.49.4.529.14431 · Loewenstein, Thompson & Gentner 1999, *Psychon. Bull. Rev.*, 10.3758/BF03212967 ·
ElShenawy 2010, *J. Eur. Industrial Training*, 10.1108/03090591011031719

### Conversation science and language
Huang, Yeomans, Brooks, Minson & Gino 2017, *JPSP*, 10.1037/pspi0000097 · Yeomans et al. 2019, *JPSP*, 10.1037/pspi0000220 · Brooks & John 2018, HBR (practitioner) ·
Menold 2020, *J. Official Statistics* 36(4), 10.2478/jos-2020-0041 · Hosman 1989, *HCR* 15 · Blankenship & Holtgraves 2005, *JLSP* 24 · Fragale 2006, *OBHDP* 101 ·
Jensen 2008, *HCR*, 10.1111/j.1468-2958.2008.00324.x · Tenney, MacCoun, Spellman & Hastie 2007, *Psych. Science* 18(1), 10.1111/j.1467-9280.2007.01847.x ·
Tenney, Spellman & MacCoun 2008, *JESP* · Packard & Berger 2021, *JCR* 47(5), 10.1093/jcr/ucaa038 · Larrimore et al. 2011, *JACR* 39(1) ·
Oppenheimer 2006, *Applied Cognitive Psychology*, 10.1002/acp.1178 · MacLaren et al. 2020, *Leadership Quarterly*, 10.1016/j.leaqua.2020.101409 ·
Mullen, Salas & Driskell 1989, *JESP* 25 · Woolley et al. 2010, *Science*, 10.1126/science.1193147 · Pickering & Garrod 2004, *BBS* 27 ·
Brennan & Clark 1996, *JEP:LMC*, 10.1037/0278-7393.22.6.1482 · Ireland et al. 2011, *Psych. Science* · Taylor & Thomas 2008, *NCMR*, 10.1111/j.1750-4716.2008.00016.x ·
Soliz & Giles 2014, *Communication Yearbook* 38 · Yeomans, Minson, Collins, Chen & Gino 2020, *OBHDP* 160, 10.1016/j.obhdp.2020.03.011 ·
Stivers et al. 2009, *PNAS*, 10.1073/pnas.0903616106 · Levinson & Torreira 2015, *Frontiers in Psychology*, 10.3389/fpsyg.2015.00731 ·
Roberts & Francis 2013, *JASA* 133 · Roberts, Margutti & Takano 2011, *Discourse Processes* 48 · Templeton et al. 2022, *PNAS*, 10.1073/pnas.2116915119 ·
Thomas & Kaschak 2025, *PBR*, 10.3758/s13423-025-02760-z · Tanveer, Lin & Hoque 2015 (Rhema), IUI, 10.1145/2678025.2701386 ·
Damian et al. 2015 (Logue), CHI, 10.1145/2702123.2702314 · Zulfikar et al. 2024 (Memoro), CHI, 10.1145/3613904.3642450 ·
Keysar, Hayakawa & An 2012, *Psych. Science*, 10.1177/0956797611432178 · Costa et al. 2014, *PLoS ONE*, 10.1371/journal.pone.0094842 ·
Circi, Gatti, Russo & Vecchi 2021, *PBR* 28 · Lev-Ari & Keysar 2010, *JESP*

### Sales and client service
Rackham 1988, *SPIN Selling* (practitioner; 35,000 observed calls, never peer-reviewed) · Dixon & Adamson 2011, *The Challenger Sale* (practitioner) ·
Rapp, Bachrach, Panagopoulos & Ogilvie 2014, critique of the Challenger model, *JPSSM* 34(4) · Fitzpatrick 2013, *The Mom Test*; Blank 2005 (practitioner) ·
Franke & Park 2006, *JMR* 43(4), 10.1509/jmkr.43.4.693 · Verbeke, Dietz & Verwaal 2011, *JAMS* 39(3), 10.1007/s11747-010-0211-8 ·
Wieseke, Alavi & Habel 2014, *J. Marketing* 78(6) · Alavi, Wieseke & Guba 2016, *J. Retailing* 92(1), 10.1016/j.jretai.2015.08.002 ·
Alavi et al. 2018, *JAMS*, 10.1007/s11747-017-0566-1 · Gelbrich & Roschk 2011, *J. Service Research* 14(1), 10.1177/1094670510387914 ·
Roschk & Kaiser 2013, *Marketing Letters* 24(3), 10.1007/s11002-012-9218-x · Davidow 2003, *J. Service Research* 5(3), 10.1177/1094670502238917 ·
Tax, Brown & Chandrashekaran 1998, *J. Marketing* 62(2) · Smith, Bolton & Wagner 1999, *JMR* 36(3) · Keaveney 1995, *J. Marketing* 59(2) ·
Dixon, Freeman & Toman 2010, HBR (CEB survey, not peer-reviewed) · Komal et al. 2020, *IEEE Access* 8, 10.1109/ACCESS.2020.3007098 ·
Schmidt & Bijmolt 2020, *JAMS* 48(3), 10.1007/s11747-019-00666-6 · Murphy et al. 2005 and List & Gallet 2001, *Environmental & Resource Economics* ·
Morwitz, Steckel & Gupta 2007, *Int. J. Forecasting* 23(3), 10.1016/j.ijforecast.2007.05.015 · Bonaccio & Dalal 2006, *OBHDP* 101(2), 10.1016/j.obhdp.2006.07.001 ·
Sniezek & Van Swol 2001, *OBHDP* 84(2) · Price & Stone 2004, *J. Behavioral Decision Making* 17(1) ·
Gong (tier C, vendor): best time to talk price and budget · sales demos (67,149) · discovery calls (519k) · talk-to-listen ratio (2016, 2025 refresh) · next steps (8,382 deals) · best insights of 2025

### Learning, motivation, measurement, AI judges
Finkelstein & Fishbach 2012, *JCR* 39(1), 10.1086/661934 · Deci, Koestner & Ryan 1999, *Psychological Bulletin* 125(6) ·
Locke & Latham 2002, *American Psychologist* 57(9), 10.1037/0003-066X.57.9.705; 2019, *Motivation Science*, 10.1037/mot0000127 ·
Gollwitzer & Sheeran 2006, *Adv. Exp. Soc. Psych.* 38, 10.1016/S0065-2601(06)38002-1 · Seijts & Latham 2005, *Acad. Mgmt Executive* 19(1) · Winters & Latham 1996, *GOM* 21(2) ·
Roediger & Karpicke 2006, *Psych. Science* 17(3), 10.1111/j.1467-9280.2006.01693.x · Dunlosky et al. 2013, *PSPI* 14(1), 10.1177/1529100612453266 ·
Cepeda et al. 2006, *Psych. Bulletin* 132(3); 2008, *Psych. Science* 19(11), 10.1111/j.1467-9280.2008.02209.x · Moore et al. 2018, Cochrane, 10.1002/14651858.CD003751.pub4 ·
Burke & Hutchins 2007, *HRD Review* 6(3), 10.1177/1534484307303035 · Robbrecht et al. 2025, *BMC Medical Education*, 10.1186/s12909-024-06515-7 ·
Ericsson, Krampe & Tesch-Römer 1993, *Psychological Review* 100(3) · Sailer & Homner 2020, *Educ. Psych. Review* 32, 10.1007/s10648-019-09498-w ·
Koivisto & Hamari 2019, *IJIM* 45 · Mekler et al. 2017, *Computers in Human Behavior* 71, 10.1016/j.chb.2015.08.048 ·
Ryan, Rigby & Przybylski 2006, *Motivation and Emotion* 30 · Silverman & Barasch 2023, *JCR* 49(6), 10.1093/jcr/ucac029 ·
Lally et al. 2010, *Eur. J. Soc. Psych.* 40(6), 10.1002/ejsp.674 · Wood & Neal 2007, *Psychological Review* 114(4) ·
Smith & Kendall 1963, *JAP* 47(2), 10.1037/h0047060 · Kinicki, Bannister, Hom & DeNisi 1985, *EPM* 45(3) · Landy & Farr 1980, *Psych. Bulletin* 87 ·
Kell et al. 2017, ETS Research Report, 10.1002/ets2.12152 · Pelánek 2016, *Computers & Education* 98, 10.1016/j.compedu.2016.03.017 ·
Klinkenberg et al. 2011, *Computers & Education* 57 · Glickman 1999, *JRSS-C* 48 · Zheng et al. 2023, NeurIPS D&B, arXiv:2306.05685 ·
Liu et al. 2023 (G-Eval), EMNLP · Ye et al. 2025 (CALM), ICLR, arXiv:2410.02736 · Norman, Rivera & Hughes 2026, arXiv:2606.19544 ·
Hoque et al. 2013 (MACH), UbiComp · Ofek, Iqbal & Strauss 2013, CHI, 10.1145/2470654.2466425 · Samrose, Rawassizadeh & Hoque 2020, arXiv:2011.06529 ·
Hancock, Naaman & Levy 2020, *JCMC* 25(1), 10.1093/jcmc/zmz022 · Hohenstein et al. 2023, *Scientific Reports* 13:5487, 10.1038/s41598-023-30938-9 · Zhu et al. 2026, arXiv:2602.12089

### Could not verify (not used as evidence)
Anderson & Balzer 1991 (findings not retrieved) · Burrell & Koper 1998 hedging meta-analysis (chapter not accessed) · Orr & Guthrie pooled anchor coefficient ·
Hüffmeier 2014 pooled d (abstract only) · Macnamara & Maitra 2019 effect sizes · Krippendorff 2004 thresholds (secondary sources) ·
"Logue 2021" (does not exist; Logue is Damian et al. 2015) · Gong's "15–16 vs 20 questions" and "close rates fall 71 % without next steps" (secondary blogs) ·
Rackham's 72→76 % and 42→33 % closing figures (book only) · Duolingo streak retention (company blogs) · any peer-reviewed study of L2 hedging in business meetings,
of compound questions in spoken dialogue, or of reading a prompt during live dialogue · Maister, *The Trusted Advisor* (no empirical test) · Radical Candor (no peer-reviewed test)
