  
＜Revision History＞

| Revision | Publication Date | Approval | Collation | Creating |
| :---- | :---- | :---- | :---- | :---- |
| 0.1 | OCT-27-2026 | \- | \- | nhannh18 |

＜Revision content＞

| Revision | No | Revision content |
| :---- | :---- | :---- |
| 0.1 | \- | Tạo mới: Verification strategy cho block LDPC codec (UVM, SVA kiểm tra port, VCS, Verdi) |

**＜Table of contents＞**

**[1\.](#introduction)**	[**Introduction**](#introduction)  
[1.1.	About this book](#about-this-book)  
[1.1.1.	Document structure](#document-structure)  
[1.1.2.	Attached document](#attached-document)  
[1.2.	Input documents](#input-documents)  
[1.3.	Output documents](#output-documents)  
[1.4.	Abbreviation](#abbreviation:)  
[1.5.	Notation](#notation:)  
[1.5.1.	Mark of numeral](#mark-of-numeral:)  
[1.5.2.	Mark of signal state](#mark-of-signal-state:)  
[1.5.3.	Mark of data size](#mark-of-data-size:)  
[1.5.4.	Other mark](#other-mark:)

[**2\.**	**Verification strategy**](#verification-strategy:)  
[2.1.	Outline](#outline:)  
[2.2.	Policies](#policies:)  
[2.2.1.	Verification level](#verification-level:)  
[2.2.2.	Verification goal](#verification-goal:)  
[2.2.3.	Verification priority](#verification-priority:)  
[2.2.4.	Verification methodology/EDA](#verification-methodology/eda:)  
[2.3.	Schedule](#schedule:)  
[2.4.	Test-bench](#test-bench:)

**＜Table of figures＞**  
[Figure 2.3‑1: Verification schedule](#figure-2.3‑1:-verification-schedule)  
[Figure 2.4‑1: DUV test-bench](#figure-2.4‑1:-duv-test-bench)

**＜Table of tables＞**  
[Table 1.1‑1: Structure of this document](#table-1.1‑1:-structure-of-this-document)  
[Table 1.1‑2: Attached documents list](#table-1.1‑2:-attached-documents-list)  
[Table 1.2‑1: Input documents list](#table-1.2‑1:-input-documents-list)  
[Table 1.3‑1: List of output documents](#table-1.3‑1:-list-of-output-documents)  
[Table 1.4‑1: Abbreviation](#table-1.4‑1:-abbreviation)  
[Table 1.5‑1: Mark of numeral](#table-1.5‑1:-mark-of-numeral)  
[Table 1.5‑2: Mark of signal state](#table-1.5‑2:-mark-of-signal-state)  
[Table 1.5‑3: Mark of data size](#table-1.5‑3:-mark-of-data-size)  
[Table 1.5‑4: Mark of bus](#table-1.5‑4:-mark-of-bus)  
[Table 2.1‑1: DUV port list (giả định)](#table-2.1‑1:-duv-port-list)  
[Table 2.2‑1: Code coverage target](#table-2.2‑1:-code-coverage-target)  
[Table 2.2‑2: Functional coverage items](#table-2.2‑2:-functional-coverage-items)  
[Table 2.2‑3: Port assertion list](#table-2.2‑3:-port-assertion-list)  
[Table 2.2‑4: Verification priority](#table-2.2‑4:-verification-priority)  
[Table 2.2‑5: EDA tool](#table-2.2‑5:-eda-tool)  
[Table 2.4‑1: Test-bench component list](#table-2.4‑1:-test-bench-component-list)

1. # **Introduction** {#introduction}

   1. ## **About this book** {#about-this-book}

      1. ### **Document structure** {#document-structure}

Tổng quan về tài liệu và từng chương được trình bày trong Table 1.1‑1.

Table 1.1‑1: Structure of this document

| Chapter | Title | Overview | Note |
| :---- | :---- | :---- | :---- |
| 1 | Introduction | Thông tin chung về tài liệu: tài liệu đầu vào, đầu ra, từ viết tắt, quy ước ký hiệu |  |
| 2 | Verification strategy | Chiến lược kiểm định block LDPC: phạm vi, mục tiêu, coverage, assertion, phương pháp UVM, công cụ VCS/Verdi, lịch trình và cấu trúc test-bench |  |

2. ### **Attached document** {#attached-document}

Danh sách tài liệu đính kèm được trình bày trong Table 1.1‑2.

Table 1.1‑2: Attached documents list

| No. | Appendix number | Title | Content |
| :---- | :---- | :---- | :---- |
| 1 | \- | \- | \- |

2. ## **Input documents** {#input-documents}

Danh sách tài liệu đầu vào được trình bày trong Table 1.2‑1.

Table 1.2‑1: Input documents list

| No. | Document name | Issuer | Version | Described name in the book | Note |
| :---- | :---- | :---- | :---- | :---- | :---- |
| 1 | LDPC\_Design\_Spec (TBD) | Design team | TBD | Design specification | Mô tả chức năng, port, timing của DUV |
| 2 | Chuẩn LDPC áp dụng (TBD, VD: IEEE 802.11 / DVB-S2 / 5G NR) | Standard body | TBD | LDPC standard | Ma trận kiểm tra chẵn lẻ H, code rate, block length |
| 3 | LDPC\_Golden\_Model (TBD, C/Matlab) | Algorithm team | TBD | Golden model | Dùng làm reference model qua DPI-C |

3. ## **Output documents** {#output-documents}

Các tài liệu bàn giao được trình bày trong Table 1.3‑1.

Table 1.3‑1: List of output documents

| No. | Document name | Issuer | File type | Release schedule | Note |
| :---- | :---- | :---- | :---- | :---- | :---- |
| 1 | Verification strategy | nhannh18 | Markdown / Microsoft word | W1 | Tài liệu này |
| 2 | Verification items | TBD | Microsoft excel | W2 | Danh sách item kiểm định, map sang coverage/assertion |
| 3 | Verification scenario spec | TBD | Microsoft excel | W3 | Mô tả test case, sequence, điều kiện pass/fail |
| 4 | Verification result report | TBD | Microsoft excel | W10 | Kết quả regression, code/functional/assertion coverage (URG) |
| 5 | Verification environment instruction document | TBD | Microsoft word | W10 | Hướng dẫn build, chạy test bằng VCS và debug bằng Verdi |

4. ## **Abbreviation:** {#abbreviation:}

* Các từ viết tắt sử dụng trong tài liệu được trình bày trong Table 1.4‑1.

Table 1.4‑1: Abbreviation

| No. | Abbreviation | Meaning |
| :---- | :---- | :---- |
| 1 | LDPC | Low-Density Parity-Check |
| 2 | DUV | Design Under Verification |
| 3 | UVM | Universal Verification Methodology |
| 4 | SVA | SystemVerilog Assertions |
| 5 | DPI | Direct Programming Interface |
| 6 | VIP | Verification IP |
| 7 | RAL | Register Abstraction Layer |
| 8 | AXIS | AXI4-Stream |
| 9 | APB | Advanced Peripheral Bus |
| 10 | LLR | Log-Likelihood Ratio |
| 11 | BER / FER | Bit Error Rate / Frame Error Rate |
| 12 | FSDB | Fast Signal Database (định dạng waveform của Verdi) |
| 13 | KDB | Knowledge Database (database thiết kế cho Verdi) |
| 14 | URG | Unified Report Generator (công cụ report coverage của VCS) |
| 15 | CRV | Constrained Random Verification |

5. ## **Notation:** {#notation:}

* Quy ước ký hiệu sử dụng trong tài liệu được trình bày dưới đây.

  1. ### **Mark of numeral:** {#mark-of-numeral:}

* Ký hiệu số được trình bày trong Table 1.5‑1.

Table 1.5‑1: Mark of numeral

| No. | Cardinal number | Description | Example |
| :---- | :---- | :---- | :---- |
| 1 | Hexadecimal numbers | Trong software: dùng tiền tố 0x | 0xA |
|  |  | Trong hardware: dùng tiền tố 'h/'H | 'hA |
| 2 | Binary numbers | Dùng tiền tố 'b/'B | 'b1010 |
| 3 | Decimal numbers | Không dùng tiền tố | 10 |

2. ### **Mark of signal state:** {#mark-of-signal-state:}

* Ký hiệu trạng thái tín hiệu được trình bày trong Table 1.5‑2.

Table 1.5‑2: Mark of signal state

| No | Term | Meaning | Remarks |
| :---- | :---- | :---- | :---- |
| 1 | Active | Tín hiệu có hiệu lực |  |
| 2 | Inactive | Tín hiệu không có hiệu lực |  |
| 3 | Asserting | Kích hoạt tín hiệu |  |
| 4 | Negating | Làm tín hiệu mất hiệu lực |  |

3. ### **Mark of data size:** {#mark-of-data-size:}

* Ký hiệu kích thước dữ liệu được trình bày trong Table 1.5‑3.

Table 1.5‑3: Mark of data size

| No | Data size | Meaning | Remarks |
| :---- | :---- | :---- | :---- |
| 1 | Byte | 8 bits |  |
| 2 | Half word | 16 bits |  |
| 3 | Word | 32 bits |  |
| 4 | Double word | 64 bits |  |

4. ### **Other mark:** {#other-mark:}

* Ký hiệu bus được trình bày trong Table 1.5‑4.

Table 1.5‑4: Mark of bus

| No | Term | Meaning | Remarks |
| :---- | :---- | :---- | :---- |
| 1 | \[m:n\] | Từ m đến n, tăng/giảm 1 đơn vị. VD: \[2:5\] biểu diễn 2, 3, 4 và 5 |  |

2. # **Verification strategy:** {#verification-strategy:}

   1. ## **Outline:** {#outline:}

* DUV là block LDPC codec, gồm:
  * **Encoder**: nhận khối bit thông tin (K bit), sinh codeword (N bit) theo ma trận kiểm tra H của chuẩn áp dụng.
  * **Decoder**: nhận LLR của codeword (N giá trị, mỗi giá trị Q bit), giải mã lặp (VD: min-sum / layered), xuất K bit thông tin, kèm trạng thái: số vòng lặp, cờ parity check pass/fail.
  * **Configuration**: chọn code rate, block length (lifting size / base graph), số vòng lặp tối đa, chế độ early termination qua thanh ghi APB.
* Mục tiêu: chứng minh DUV đúng chức năng so với golden model (bit-exact) trên toàn bộ cấu hình hỗ trợ, đúng giao thức tại mọi port, và đạt coverage target.
* Danh sách port giả định được trình bày trong Table 2.1‑1. **Cần cập nhật theo design spec chính thức.**

Table 2.1‑1: DUV port list (giả định)

| No. | Port group | Signal | Direction | Description |
| :---- | :---- | :---- | :---- | :---- |
| 1 | Clock/Reset | clk, rst\_n | Input | Clock hệ thống, reset bất đồng bộ tích cực mức thấp |
| 2 | Config (APB) | psel, penable, pwrite, paddr, pwdata, prdata, pready, pslverr | In/Out | Truy cập thanh ghi cấu hình, trạng thái |
| 3 | Input stream (AXIS slave) | s\_axis\_tvalid, s\_axis\_tready, s\_axis\_tdata, s\_axis\_tlast, s\_axis\_tuser | In/Out | Dữ liệu vào: bit thông tin (encode) hoặc LLR (decode) |
| 4 | Output stream (AXIS master) | m\_axis\_tvalid, m\_axis\_tready, m\_axis\_tdata, m\_axis\_tlast, m\_axis\_tuser | Out/In | Dữ liệu ra: codeword (encode) hoặc bit đã giải mã (decode) |
| 5 | Status/Interrupt | done, irq, dec\_fail, iter\_cnt | Output | Báo hoàn thành, lỗi giải mã, số vòng lặp đã dùng |

   2. ## **Policies:** {#policies:}

      1. ### **Verification level:** {#verification-level:}

* DUV block verification (block LDPC codec top level).
* Có thể chạy thêm sub-block level cho decoder core (check node / variable node unit) nếu cần tăng tốc closure coverage.

  2. ### **Verification goal:** {#verification-goal:}

1. #### **Scope:**

* Black-box verification: so sánh dữ liệu output với golden model qua scoreboard, kiểm tra giao thức tại tất cả port.
* White-box verification: kiểm tra giá trị thanh ghi trạng thái nội bộ (qua RAL), bộ đếm vòng lặp, FSM điều khiển và tín hiệu early termination bằng SVA bind.
* Ngoài phạm vi: đánh giá hiệu năng BER/FER dài hạn (thuộc algorithm team), kiểm tra gate-level, power-aware.

2. #### **Configuration/mode:**

* Kiểm định tất cả chế độ hoạt động: encode, decode.
* Tất cả code rate và block length mà DUV hỗ trợ (theo design spec).
* Số vòng lặp tối đa: giá trị min, max và giá trị ngẫu nhiên; early termination bật/tắt.
* Chuyển cấu hình giữa các frame liên tiếp (back-to-back) và reset giữa chừng.

3. #### **Item:**

* Code coverage:
  * Target được trình bày trong Table 2.2‑1. Thu thập bằng VCS (`-cm line+cond+fsm+tgl+branch+assert`) và report bằng URG.

Table 2.2‑1: Code coverage target

| No. | Coverage item | Target | Note |
| :---- | :---- | :---- | :---- |
| 1 | Toggle | 100% cho input/output port của top | Bit không dùng phải có waiver |
| 2 | Line | 100% | Code không với tới phải có waiver kèm lý do |
| 3 | Cond | 100% |  |
| 4 | Branch | 100% |  |
| 5 | FSM | 100% state và transition | FSM điều khiển encode/decode |
| 6 | Assertion | 100% assertion được kích hoạt (attempted), 0 lỗi | Cover property cho từng assertion |

* Functional coverage:
  * Tất cả item trong tài liệu Verification items phải được cover 100%. Các covergroup chính trong Table 2.2‑2.

Table 2.2‑2: Functional coverage items

| No. | Covergroup | Coverpoint / Cross | Note |
| :---- | :---- | :---- | :---- |
| 1 | cg\_config | mode × code\_rate × block\_length | Cross toàn bộ cấu hình hợp lệ |
| 2 | cg\_iteration | max\_iter (min/max/random), iter\_cnt thực tế, early termination bật/tắt | Bin cho giải mã thành công ở vòng đầu, vòng cuối, không hội tụ |
| 3 | cg\_channel | Mức nhiễu (SNR bin), số bit lỗi đưa vào, LLR bão hoà (giá trị max/min) | Cho decoder |
| 4 | cg\_axis\_traffic | Back-pressure trên m\_axis\_tready, khoảng trống tvalid, frame back-to-back | Cho cả 2 port stream |
| 5 | cg\_apb | Đọc/ghi từng thanh ghi, truy cập địa chỉ không hợp lệ, ghi khi đang busy | Sinh tự động từ RAL nếu có |
| 6 | cg\_reset | Reset khi idle, khi đang nhận input, khi đang xuất output | |

* Port check (SVA):
  * Mỗi interface của DUV có một module assertion riêng, gắn vào interface UVM hoặc dùng `bind` vào DUV. Danh sách assertion trong Table 2.2‑3.
  * Mỗi `assert property` có một `cover property` tương ứng để chứng minh assertion đã được kích hoạt.
  * Assertion được tắt trong reset bằng `disable iff (!rst_n)`, trừ các assertion kiểm tra giá trị trong reset.

Table 2.2‑3: Port assertion list

| No. | Port group | Assertion | Mô tả |
| :---- | :---- | :---- | :---- |
| 1 | Clock/Reset | ast\_rst\_out\_value | Trong reset, m\_axis\_tvalid, done, irq, pslverr = 0 |
| 2 | Clock/Reset | ast\_no\_x\_after\_reset | Sau khi negate rst\_n, mọi output không có X/Z (`!$isunknown`) |
| 3 | AXIS slave/master | ast\_valid\_stable | tvalid đã assert thì giữ đến khi tready = 1 (`tvalid && !tready |=> tvalid`) |
| 4 | AXIS slave/master | ast\_data\_stable | Khi tvalid && !tready, tdata/tlast/tuser giữ nguyên ở chu kỳ sau (`$stable`) |
| 5 | AXIS slave/master | ast\_no\_x\_when\_valid | Khi tvalid = 1, tdata/tlast không có X/Z |
| 6 | AXIS master | ast\_frame\_length | Số beat từ beat đầu đến tlast đúng bằng độ dài frame theo cấu hình (N cho encode, K cho decode) |
| 7 | AXIS slave | ast\_tready\_no\_x | s\_axis\_tready không bao giờ X/Z sau reset |
| 8 | APB | ast\_apb\_setup\_access | psel && !penable \|=> psel && penable (setup phase sang access phase) |
| 9 | APB | ast\_apb\_stable | Trong access phase, paddr/pwrite/pwdata giữ nguyên đến khi pready = 1 |
| 10 | APB | ast\_apb\_pslverr | pslverr chỉ assert cùng chu kỳ với pready |
| 11 | Status | ast\_done\_pulse | done là xung 1 chu kỳ, assert sau beat tlast cuối cùng của output |
| 12 | Status | ast\_iter\_range | iter\_cnt ≤ max\_iter đã cấu hình |
| 13 | Status | ast\_dec\_fail\_iter | dec\_fail = 1 suy ra iter\_cnt = max\_iter |
| 14 | Status | ast\_irq\_cause | irq chỉ assert khi done hoặc dec\_fail và interrupt được enable |
| 15 | Config | ast\_cfg\_stable\_busy | Thanh ghi cấu hình không đổi khi DUV đang xử lý frame (hoặc lệnh ghi bị chặn theo spec) |

* Timing check:
  * Kiểm tra latency từ beat input cuối đến beat output đầu nằm trong giới hạn spec, bằng SVA và scoreboard.
  * Kiểm tra throughput khi không có back-pressure (số chu kỳ trên mỗi frame).
* Connection check:
  * Kiểm tra kết nối từ top LDPC đến encoder core, decoder core, register block bằng SVA bind (nếu có sub-block).
* Synchronizer circuit check:
  * Không áp dụng nếu DUV chỉ có một clock domain. Nếu có nhiều clock domain (VD: clock APB riêng), kiểm tra input/output của synchronizer bằng SVA.
* Data check:
  * Encoder: so sánh bit-exact codeword với golden model; kiểm tra H × c^T = 0.
  * Decoder: so sánh bit-exact bit giải mã, iter\_cnt, dec\_fail với golden model (cùng thuật toán và độ rộng bit fixed-point).
  * Loopback: encoder → mô hình kênh (thêm nhiễu) → decoder, kiểm tra bit giải mã khớp với dữ liệu gốc khi nhiễu dưới ngưỡng sửa lỗi.
  * Kiểm tra giá trị thanh ghi trạng thái sau mỗi frame qua RAL.

  3. ### **Verification priority:** {#verification-priority:}

* Thứ tự ưu tiên được trình bày trong Table 2.2‑4.

Table 2.2‑4: Verification priority

| Priority | Nội dung |
| :---- | :---- |
| 1 | Reset, truy cập thanh ghi APB, port assertion cơ bản (luôn bật trong mọi test) |
| 2 | Encode với cấu hình mặc định, dữ liệu direct (all-0, all-1, pattern) |
| 3 | Decode với cấu hình mặc định, không nhiễu và nhiễu thấp |
| 4 | Toàn bộ code rate và block length, random data (CRV) |
| 5 | Decode với nhiễu gần ngưỡng, không hội tụ (dec\_fail), early termination, LLR bão hoà |
| 6 | Kết hợp: back-pressure, frame back-to-back đổi cấu hình, reset giữa chừng, loopback |
| 7 | Closure coverage: bổ sung test cho các hole, review waiver |

  4. ### **Verification methodology/EDA:** {#verification-methodology/eda:}

1. #### **Environment:**

* Tạo mới môi trường UVM (SystemVerilog IEEE 1800, UVM-1.2).
* Reuse/Modify: AXI4-Stream agent và APB agent nếu đã có trong thư viện VIP nội bộ; nếu không có thì tạo mới.
* Golden model C/Matlab của algorithm team, gọi qua DPI-C.

2. #### **Methodology:**

* UVM, constrained random verification kết hợp direct test cho các case cơ bản và corner case.
* Coverage-driven verification: closure dựa trên code coverage, functional coverage và assertion coverage.
* Assertion-based verification: SVA cho toàn bộ port (Table 2.2‑3) và một số kiểm tra white-box.
* Regression: chạy toàn bộ test với nhiều seed, merge coverage bằng URG.

3. #### **EDA tool:**

* Công cụ sử dụng trên máy vsi-sandbox-01 được trình bày trong Table 2.2‑5.

Table 2.2‑5: EDA tool

| No. | Tool | Version | Mục đích | License |
| :---- | :---- | :---- | :---- | :---- |
| 1 | Synopsys VCS | W-2024.09-SP2 (mặc định) | Compile, mô phỏng, thu thập coverage | VCS compile/runtime: 31 (dùng chung toàn máy) |
| 2 | Synopsys Verdi | W-2024.09-SP2-5-HP (mặc định) | Debug waveform FSDB, UVM debug, assertion debug, xem coverage | Verdi-3-Apex-Pkg: 26 (dùng chung) |
| 3 | URG | Đi kèm VCS W-2024.09-SP2 | Merge và report coverage | VT\_CoverageURG: 65 (dùng chung) |
| 4 | UVM library | UVM-1.2 (đi kèm VCS, `-ntb_opts uvm-1.2`) | Thư viện UVM | \- |

* Môi trường: VCS, Verdi được load sẵn lúc login (`VCS_HOME`, `VERDI_HOME`, `SNPSLMD_LICENSE_FILE=27020@vsi-sandbox-01`). Thư mục chạy mô phỏng: `/sim/<dự án>/<người dùng>/`.
* Lệnh compile tham khảo:

```
vcs -full64 -sverilog -ntb_opts uvm-1.2 -timescale=1ns/1ps \
    -kdb -lca -debug_access+all \
    -cm line+cond+fsm+tgl+branch+assert -cm_dir cov/simv.vdb \
    -f filelist.f -top tb_top -l compile.log
```

* Lệnh chạy tham khảo:

```
./simv +UVM_TESTNAME=<test_name> +ntb_random_seed=<seed> \
       -cm line+cond+fsm+tgl+branch+assert -cm_name <test_name>_<seed> \
       +fsdb+dump -l sim_<test_name>_<seed>.log
```

* Debug bằng Verdi:
  * Dump waveform FSDB trong `tb_top` bằng `$fsdbDumpfile` / `$fsdbDumpvars`, bật theo plusarg (VD: `+fsdb+dump`) để regression không dump mặc định.
  * Dump thêm thông tin UVM và assertion cho Verdi (`$fsdbDumpSVA`, transaction recording) khi debug test lỗi.
  * Mở debug: `verdi -dbdir simv.daidir -ssf novas.fsdb &` để xem source, schematic, waveform, UVM component/transaction và trạng thái assertion.
  * Xem coverage: `verdi -cov -covdir cov/simv.vdb &` hoặc report HTML từ `urg -dir cov/simv.vdb -report urgReport`.

## **Schedule:** {#schedule:}

Figure 2.3‑1: Verification schedule

| Phase | Nội dung | W1 | W2 | W3 | W4 | W5 | W6 | W7 | W8 | W9 | W10 |
| :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | Verification strategy | ■ |  |  |  |  |  |  |  |  |  |
| 2 | Verification items, scenario spec |  | ■ | ■ |  |  |  |  |  |  |  |
| 3 | Xây dựng test-bench UVM, agent, SVA port, tích hợp golden model |  | ■ | ■ | ■ |  |  |  |  |  |  |
| 4 | Test cơ bản (priority 1–3) |  |  |  | ■ | ■ |  |  |  |  |  |
| 5 | Test random, corner case (priority 4–6) |  |  |  |  | ■ | ■ | ■ |  |  |  |
| 6 | Regression, closure coverage (priority 7) |  |  |  |  |  |  | ■ | ■ | ■ |  |
| 7 | Result report, environment instruction |  |  |  |  |  |  |  |  | ■ | ■ |

Lịch trình trên là dự kiến, sẽ cập nhật theo kế hoạch dự án và ngày release RTL.

## **Test-bench:** {#test-bench:}

Figure 2.4‑1: DUV test-bench

```
+--------------------------------------------------------------------------------+
| tb_top                                                                         |
|  +--------------------------------------------------------------------------+  |
|  | uvm_test (ldpc_base_test / ldpc_*_test)                          [NEW]    |  |
|  |  +--------------------------------------------------------------------+  |  |
|  |  | ldpc_env                                                   [NEW]    |  |  |
|  |  |                                                                    |  |  |
|  |  |  +--------------+   +--------------+   +--------------+            |  |  |
|  |  |  | apb_agent    |   | axis_in_agent|   | axis_out_agt |            |  |  |
|  |  |  | [REUSE/MOD]  |   | [REUSE/MOD]  |   | [REUSE/MOD]  |            |  |  |
|  |  |  | sqr/drv/mon  |   | sqr/drv/mon  |   | drv(ready)/  |            |  |  |
|  |  |  +------+-------+   +------+-------+   | mon          |            |  |  |
|  |  |         |                  |           +------+-------+            |  |  |
|  |  |  +------+-------+          |                  |                    |  |  |
|  |  |  | ldpc_ral     |          v                  v                    |  |  |
|  |  |  | [NEW]        |   +--------------------------------+             |  |  |
|  |  |  +--------------+   | ldpc_scoreboard          [NEW] |             |  |  |
|  |  |                     |   +------------------------+   |             |  |  |
|  |  |  +--------------+   |   | ref model (DPI-C)      |   |             |  |  |
|  |  |  | ldpc_cov     |   |   | golden C/Matlab [MODEL]|   |             |  |  |
|  |  |  | [NEW]        |   |   +------------------------+   |             |  |  |
|  |  |  +--------------+   +--------------------------------+             |  |  |
|  |  |  virtual_sequencer [NEW], channel model (noise/LLR gen) [MODEL]    |  |  |
|  |  +--------------------------------------------------------------------+  |  |
|  +--------------------------------------------------------------------------+  |
|        |  apb_if            |  axis_in_if          ^  axis_out_if             |
|        v  + apb_sva [NEW]   v  + axis_sva [NEW]    |  + axis_sva [NEW]        |
|  +--------------------------------------------------------------------------+  |
|  |                         DUV: LDPC codec (RTL)                            |  |
|  |       bind: ldpc_status_sva, ldpc_cfg_sva, ldpc_fsm_sva  [NEW]           |  |
|  +--------------------------------------------------------------------------+  |
|  clk/rst gen [NEW]          FSDB dump control (+fsdb+dump) [NEW]               |
+--------------------------------------------------------------------------------+
```

Legend of color:

       [NEW]           Create new

       [MODEL]         Model

       [REUSE/MOD]     Reused and Modified

* Mô tả các thành phần test-bench được trình bày trong Table 2.4‑1.

Table 2.4‑1: Test-bench component list

| No. | Component | Type | Mô tả |
| :---- | :---- | :---- | :---- |
| 1 | apb\_agent | Reused and Modified | Driver/monitor APB, cấu hình DUV và đọc trạng thái |
| 2 | ldpc\_ral | Create new | Register model, dùng cho front-door access và kiểm tra giá trị thanh ghi |
| 3 | axis\_in\_agent | Reused and Modified | Gửi bit thông tin (encode) hoặc LLR (decode), hỗ trợ chèn khoảng trống tvalid |
| 4 | axis\_out\_agent | Reused and Modified | Điều khiển tready ngẫu nhiên (back-pressure), monitor dữ liệu output |
| 5 | ldpc\_scoreboard | Create new | So sánh output DUV với golden model, kiểm tra iter\_cnt, dec\_fail, latency |
| 6 | Reference model | Model | Golden model C/Matlab của algorithm team, gọi qua DPI-C |
| 7 | Channel model | Model | Sinh nhiễu và LLR theo SNR cho decode và loopback |
| 8 | ldpc\_cov | Create new | Covergroup functional coverage (Table 2.2‑2) |
| 9 | apb\_sva, axis\_sva | Create new | Assertion kiểm tra giao thức port, gắn vào interface |
| 10 | ldpc\_status\_sva, ldpc\_cfg\_sva, ldpc\_fsm\_sva | Create new | Assertion kiểm tra status, config và FSM nội bộ, dùng `bind` vào DUV |
| 11 | virtual\_sequencer, sequence library | Create new | Điều phối cấu hình APB và stream dữ liệu cho từng test |
| 12 | tb\_top | Create new | Sinh clock/reset, khởi tạo interface, DUV, điều khiển dump FSDB |
