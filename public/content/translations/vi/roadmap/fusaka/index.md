---
title: Fulu-Osaka (Fusaka)
description: "Tìm hiểu về nâng cấp giao thức Fusaka"
lang: vi
---

# Fusaka <Emoji text="🦓" /> {#fusaka}

**Bản nâng cấp Fusaka rất được mong đợi của Ethereum đã đi vào hoạt động vào ngày 3 tháng 12 năm 2025**

Nâng cấp mạng lưới Fusaka trong giao đoạn [Pectra](/roadmap/pectra/) và mang tới nhiều tính năng và cải thiện cho người dùng Ethereum và lập trình viên. Cái lên bao gồm nâng cấp lớp thực thi Osaka và bản của lớp đồng thuận được đặt theo tên sao Fulu. Cả hai phần của Ethereum sẽ nhận nâng cấp giúp Ethereum mở rộng, bảo mật và cải thiện trải nghiệm người dùng trong tương lai.

<Alert variant="update">
<AlertContent>
<AlertDescription>
Bản nâng cấp Fusaka chỉ là một bước duy nhất trong các mục tiêu phát triển dài hạn của Ethereum. Tìm hiểu thêm về [lộ trình giao thức](/roadmap/) và [các bản nâng cấp trước đó](/ethereum-forks/).
</AlertDescription>
</AlertContent>
</Alert>

## Những cải tiến trong Fusaka {#improvements-in-fusaka}

### Mở rộng quy mô blob {#scale-blobs}

#### PeerDAS {#peerdas}

Đây là _điểm nhấn_ của bản fork Fusaka, tính năng chính được thêm vào trong bản nâng cấp này. Hiện tại lớp 2 đăng dữ liệu của mình lên Ethereum dưới dạng Blob, một loại dữ liệu tạm thời được tạo riêng cho lớp 2. Trước Fusaka, mọi nút đầy đủ đều phải lưu trữ tất cả Blob để đảm bảo rằng dữ liệu tồn tại. Khi thông lượng blob tăng lên, việc phải tải xuống toàn bộ dữ liệu này trở nên cực kỳ tốn kém tài nguyên.

Với phương pháp [lấy mẫu khả dụng dữ liệu (Data Availability Sampling)](https://notes.ethereum.org/@fradamt/das-fork-choice) thay vì phải lưu toàn bộ dữ liệu Blob, mỗi nút sẽ chỉ chịu trách nhiệm cho một phần của dữ liệu Blob. Các Blob được phân phối ngẫu nhiên đồng đều giữa các nút trong mạng, với mỗi nút đầy đủ chỉ giữ 1/8 dữ liệu, từ đó về mặt lý thuyết cho phép mở rộng lên tới 8 lần. Để đảm bảo tính khả dụng của dữ liệu, bất kỳ phần nào của dữ liệu cũng có thể được tái tạo từ 50% dữ liệu hiện có bằng các phương pháp giúp giảm xác suất dữ liệu sai hoặc thiếu xuống mức không đáng kể về mặt mật mã học (~ một trong 10<sup>20</sup> đến một trong 10<sup>24</sup>).

Việc này giúp yêu cầu phần cứng và băng thông cần thiết cho mỗi nút vẫn ở mức chấp nhận được, đồng thời cho phép mở rộng Blob mang lại khả năng mở rộng với phí thấp hơn cho lớp 2.

[Tìm hiểu thêm về PeerDAS](/roadmap/fusaka/peerdas/)

**Tài nguyên**:

- [Thông số kỹ thuật EIP-7594](https://eips.ethereum.org/EIPS/eip-7594)
- [DappLion về PeerDAS: Mở rộng quy mô Ethereum ngay hôm nay | ETHSofia 2024](https://youtu.be/bONWd1x2TjQ?t=328)
- [Học thuật: Tài liệu về PeerDAS của Ethereum (PDF)](https://eprint.iacr.org/2024/1362.pdf)

#### Các bản fork chỉ dành cho tham số blob {#blob-parameter-only-forks}

Mở rộng lớp 2 của Ethereum - cũng như là giúp mạng lưới phát triên, họ cần phải đăng nhiều dữ liệu lên mạng Ethereum. Điều này có nghĩa rằng Ethereum sẽ cần phải năng số Blob khả dụng khi thời gian trôi qua. Mặc dù PeerDAS cho phép mở rộng dữ liệu Blob, nó cần phải tăng dần đều và an toàn.

Vì Ethereum là mã nguồn chạy trên hàng nghìn nút độc lập yêu cầu sự đồng thuận về các quy tắc giống nhau, chúng ta không thể chỉ đơn giản giới thiệu các thay đổi như tăng số lượng blob theo cách bạn triển khai một bản cập nhật trang web. Bất kì thay đổi nào về mặt quy tắt phải được thực hiện dưới dạng một bản nâng cáp có phối hợp, trong đó mọi nút, Client và phần mềm xác thực cần phải nâng cấp trước cùng một nút đã xác định trước.

Những đợt nâng cấp có phối hợp này thường bao gồm rất nhiều thay đổi, trải qua rất nhiều kiểm nghiệm, do đó rất tốn thời gian. Để thích ứng nhanh đến nhu cầu Blob của lớp 2, các Fork điều chỉnh tham số Blob giới thiệu cơ chế cho phép tăng số lượng Blob mà không phải chờ theo lịch nâng cấp.

Các Fork điều chỉnh tham số Blob có thể được thiết lập bởi các Client, tương tự như cấu hình khác chẳng hạn như giới hạn Gas. Trong thời gian giữa các nâng cấp lớn của Ethereum, Client có thể đồng tình tăng `mục tiêu` và số Blob `tối đa` lên chẳng hạn như 9 và 12 và sau đó nhà vận hành nút sẽ tham gia để cập nhật vòa Fork nhỏ này. Các Fork điều chỉnh tham số Blob này có thể được cấu hình bất cứ lúc nào.

Khi các blob lần đầu tiên được thêm vào mạng trong bản nâng cấp Dencun, mục tiêu là 3. Con số đó đã được tăng lên 6 trong Pectra và, sau Fusaka, giờ đây con số đó có thể được tăng với tốc độ bền vững độc lập với các bản nâng cấp mạng chính này.

![Biểu đồ hiển thị số lượng blob trung bình trên mỗi khối và các mục tiêu gia tăng với các bản nâng cấp](./average-blob-count-per-block.webp)

Nguồn biểu đồ: [Ethereum Blobs - @hildobby, Dune Analytics](https://dune.com/hildobby/blobs)

**Tài nguyên**: [Thông số kỹ thuật EIP-7892](https://eips.ethereum.org/EIPS/eip-7892)

#### Phí cơ bản của Blob bị giới hạn bởi chi phí thực thi {#blob-base-fee-bounded-by-execution-costs}

Khi đăng dữ liệu, các lớp 2 phải trả hai loại phí: phí Blob và phí Gas thực thi cần thiết để xác minh các Blob đó. Nếu chi phí Gas thực thi chiếm ưu thế, thì cơ chế đấu giá phí Blob có thể tụt xuống mức 1 Wei và không còn đóng vai trò là tín hiệu giá nữa.

EIP-7918 đặt một mức tỷ lệ giá sàn cho mỗi Blob. Khi giá dự trữ cao hơn phí cơ bản danh nghĩa của blob, thuật toán điều chỉnh phí sẽ coi khối đó là vượt mục tiêu, ngừng đẩy phí xuống và cho phép nó tăng lên bình thường. Kết quả là:

- thị trường phí Blob luôn phản ứng trước tình trạng tắt nghẽn
- lớp 2 sẽ phải chịu giúp một phần chi phí tính toán mà chúng bắt buộc các nút phải gánh chịu
- các đợt tăng đột biến phí cơ bản trên lớp thực thi sẽ không còn có thể kẹt phí Blob ở mức dưới 1 Wei nữa

**Tài nguyên**:

- [Thông số kỹ thuật EIP-7918](https://eips.ethereum.org/EIPS/eip-7918)
- [Giải thích theo kiểu kể chuyện](https://notes.ethereum.org/@anderselowsson/AIG)

### Mở rộng quy mô L1 {#scale-l1}

#### Hết hạn lịch sử và biên lai đơn giản hơn {#history-expiry}

Vào tháng 7 năm 2025, các client thực thi Ethereum [bắt đầu hỗ trợ hết hạn lịch sử một phần](https://blog.ethereum.org/2025/07/08/partial-history-exp). Điều này đã loại bỏ lịch sử cũ hơn [bản nâng cấp The Merge](https://ethereum.org/roadmap/merge/) để giảm dung lượng đĩa mà các nhà khai thác nút yêu cầu khi Ethereum tiếp tục phát triển.

EIP này nằm trong một phần tách biệt với "Các EIP cốt lõi" vì bản fork không thực sự triển khai bất kỳ thay đổi nào - đó là một thông báo rằng các nhóm client phải hỗ trợ hết hạn lịch sử trước bản nâng cấp Fusaka. Trên thực tế, các client có thể triển khai điều này bất cứ lúc nào nhưng việc thêm nó vào bản nâng cấp đã cụ thể đưa nó vào danh sách việc cần làm của họ và cho phép họ thử nghiệm các thay đổi của Fusaka cùng với tính năng này.

**Tài nguyên**: [Thông số kỹ thuật EIP-7642](https://eips.ethereum.org/EIPS/eip-7642)

#### Đặt giới hạn cho MODEXP {#set-upper-bounds-for-modexp}

Cho đến bây giờ, precompile MODEXP có thể chấp nhận các số gần như với bất kỳ kích thước nào. Điều đó khiến việc kiểm nghiệm trở nên khó khăn, dễ bị lạm dụng và gây rủi ro cho sự ổn định của Client. EIP-7823 đặt ra một giới hạn rõ ràng: mỗi số đầu vào chỉ được phép dài tối đa 8192 Bit (1024 Byte). Bất kỳ giá trị nào lớn hơn sẽ bị từ chối, Gas của giao dịch đó sẽ bị đốt, và không có thay đổi trạng thái nào xảy ra. Giới hạn này dư sức đáp ứng các nhu cầu thực tế, đồng thời loại bỏ những trường hợp cực đoan vốn gây phức tạp cho việc hoạch định giới hạn Gas và rà soát bảo mật. Thay đổi này mang lại khả năng bảo mật tốt hơn và tăng cường chống tấn công từ chối dịch vụ (DoS) mà không ảnh hưởng đến trải nghiệm người dùng hay nhà phát triển.

**Tài nguyên**: [Thông số kỹ thuật EIP-7823](https://eips.ethereum.org/EIPS/eip-7823)

#### Giới hạn cho phí Gas của giao dịch {#transaction-gas-limit-cap}

EIP-[7825](https://eips.ethereum.org/EIPS/eip-7825) đặt một giới hạn 16.777.216 (2^24) Gas mỗi giao dịch. Đây là một biện pháp chủ động chống tấn công từ chối dịch vụ (DoS) bằng cách giới hạn chi phí trong kịch bản xấu nhất của bất kỳ giao dịch đơn lẻ nào khi chúng ta nâng giới hạn Gas của khối. Điều này giúp việc mô hình hóa quá trình xác thực và lan truyền trở nên dễ dàng hơn, từ đó cho phép chúng ta xử lý vấn đề mở rộng thông qua việc tăng giới hạn Gas.

Tại sao lại chính xác là 2^24 Gas? Mức này nhỏ hơn đáng kể so với giới hạn Gas hiện tại, nhưng đủ lớn để triển khai các hợp đồng thực tế và các hợp trình biên dịch có sẵn (Precompiler) nặng, và đồng là lũy thừa của 2 nên dễ triển khai trên nhiều Client. Kích thước giao dịch tối đa mới này tương tự như kích thước khối trung bình trước Pectra, khiến nó trở thành một giới hạn hợp lý cho bất kỳ hoạt động nào trên Ethereum.

**Tài nguyên**: [Thông số kỹ thuật EIP-7825](https://eips.ethereum.org/EIPS/eip-7825)

#### Tăng chi phí gas `MODEXP` {#modexp-gas-cost-increase}

MODEXP là một hợp đồng thông minh (Precompile) tích hợp sẵn dùng để tính lũy thừa mô-đun (Modular Exponentiation) — một dạng toán học với số lớn, được sử dụng trong xác minh chữ ký RSA và các hệ thống bằng chứng. Nó cho phép các hợp đồng thông minh thực hiện trực tiếp các phép tính này mà không cần tự viết lại.

Các nhà phát triển và nhóm Client nhận định rằng MODEXP là một trở ngại lớn trong việc tăng giới hạn Gas của khối, vì cơ chế tính giá Gas hiện tại thường đánh giá thấp lượng sức mạnh tính toán cần thiết cho một số loại đầu vào nhất định. Điều này có nghĩa là một giao dịch sử dụng MODEXP có thể chiếm phần lớn thời gian xử lý của cả một khối, làm chậm toàn bộ mạng lưới.

EIP này thay đổi cách tính giá để phù hợp với chi phí tính toán thực tế bằng cách:

- tăng phí tối thiểu lên từ 200 lên 500 Gas và loại bỏ một phần ba chiết khấu từ EIP-256 trong công thức tính chi phí tổng quát
- tăng phí mạnh hơn khi đầu vào của số mũ quá dài. nếu như số mũ (sỗ mũ mà bạn thêm vào như một số thứ hai) dài hơn 32 Byte / 256 Bit, thì phí Gas sẽ tăng nhanh hơn cho mỗi Byte bổ sung
- bằng cách tính thêm phí đối với cơ số hoặc mô-đun bổ sung. Hai số còn lại (cơ số và Mô-đun) được giả định là có ít nhất 32 Byte - nếu một trong hai số này lớn hơn, chi phí sẽ tăng theo tỷ lệ thuận với kích thước của nó

Nhờ việc điều chỉnh phí sát hơn với thời gian xử lý thực tế, MODEXP sẽ không còn có khả năng khiến một khối mất quá nhiều thời gian để xác thực nữa. Thay đổi này là một trong những bước thiết kế nhằm đảm bảo tăng giới hạn phí gas cho Ethereum một cách an toàn hơn trong tương lai.

**Tài nguyên**: [Thông số kỹ thuật EIP-7883](https://eips.ethereum.org/EIPS/eip-7883)

#### Giới hạn kích thước block thực thi theo mã hóa RLP {#rlp-execution-block-size-limit}

Điều này tạo ra một giới hạn trần về kích thước của một khối - đây là giới hạn đối với những gì được _gửi_ qua mạng và tách biệt với giới hạn gas, vốn giới hạn _công việc_ bên trong một khối. Giới hạn kích thước khối là 10 MiB, với một khoản dung sai nhỏ (2 MiB) dành riêng cho dữ liệu đồng thuận để mọi thứ vừa vặn và được lan truyền một cách sạch sẽ. Nếu một khối xuất hiện lớn hơn thế, các client sẽ từ chối nó.
Điều này là cần thiết vì các khối rất lớn mất nhiều thời gian hơn để lan truyền và xác minh trên toàn mạng và có thể tạo ra các vấn đề về đồng thuận hoặc bị lạm dụng như một vector tấn công DoS. Ngoài ra, cơ chế gossip của lớp đồng thuận đã không chuyển tiếp các khối trên ~10 MiB, do đó, việc điều chỉnh lớp thực thi theo giới hạn đó sẽ tránh được các tình huống kỳ lạ “một số thấy, một số khác bỏ qua”.

Chi tiết: đây là giới hạn về kích thước khối thực thi được mã hóa [RLP](/developers/docs/data-structures-and-encoding/rlp/). Tổng cộng 10 MiB, với biên độ an toàn 2 MiB dành riêng cho việc đóng khung khối beacon. Trên thực tế, các client định nghĩa

`MAX_BLOCK_SIZE = 10,485,760` byte và

`SAFETY_MARGIN = 2,097,152` byte,

và từ chối bất kỳ khối thực thi nào có tải trọng RLP vượt quá

`MAX_RLP_BLOCK_SIZE = MAX_BLOCK_SIZE − SAFETY_MARGIN`

Mục tiêu là giới hạn thời gian lan truyền/xác thực trong trường hợp xấu nhất và phù hợp với hành vi gossip của lớp đồng thuận, giảm rủi ro tái tổ chức/DoS mà không thay đổi cách tính toán gas.

**Tài nguyên**: [Thông số kỹ thuật EIP-7934](https://eips.ethereum.org/EIPS/eip-7934)

#### Đặt giới hạn gas mặc định thành 60 triệu {#set-default-gas-limit-to-60-million}

Trước khi nâng giới hạn Gas từ 30 triệu lên 36 triệu vào tháng 2/2025 (và sau đó lên 45 triệu), giá trị này đã không thay đổi kể từ sự kiện hợp nhất (The Merge - tháng 9/2022). EIP này đặt mục tiêu ưu tiên mở rộng một cách nhất quán.

EIP-7935 phối hợp các nhóm Client của lớp thực thư để nâng giới hạn Gas mặc định lên trên mức 45 triệu hiện nay trong bản nâng cấp Fusaka. Đây là một EIP thông tin, nhưng nó nêu rõ yêu cầu Client phải thử nghiệm các mức giới hạn Gas cao hơn trên mạng của nhà lập trình (Devnet), thống nhất một giá trị an toàn, và đưa giá trị đó vào bản phát hành Fusaka.

Kế hoạch trên mạng của nhà lập trình hướng tới kiểm thử chịu tải ~60 triệu (các khối đầy đủ với môi trường giả lập) và tăng dần theo từng bước; Nghiên cứu thấy ở điều kiện xấu nhất kích thước khối không nên trở thành điểm nghẽn cổ chai dưới ~150 triệu. Việc triển khai nên đi kèm với giới hạn Gas tối đa cho một giao dịch (EIP-7825) để đảm bảo rằng không có giao dịch đơn lẻ nào kiếm ưu thế khi tăng giới hạn.

**Tài nguyên**: [Thông số kỹ thuật EIP-7935](https://eips.ethereum.org/EIPS/eip-7935)

### Cải thiện UX {#improve-ux}

#### Cơ chế xác định trước người đề xuất khối {#deterministic-proposer-lookahead}

Với EIP-7917, chuỗi Beacon sẽ nhận thức được người đề xuất khối cho chu kỳ (Epoch) sắp tới. Việc có một cách dự đoán trước về nút xác thực nào sẽ đề xuất các khối trong tương lai có thể cho phép [Preconfirmation](https://ethresear.ch/t/based-preconfirmations/17353) – tức là một cam kết với người đề xuất sắp tới rằng giao dịch của người dùng sẽ được đưa vào khối của họ mà không cần phải chờ đến khi khối thực sự được tạo ra.

Tính năng này mang lại lợi ích cho việc triển khai Client và tăng cường bảo mật cho mạng lưới, vì nó ngăn chặn các trường hợp đặc biệt nơi nút xác thực có thể thao túng lịch trình người đề xuất. Cơ chế xác định trước cũng giúp việc triển khai trở nên ít phức tạp hơn.

**Tài nguyên**: [Thông số kỹ thuật EIP-7917](https://eips.ethereum.org/EIPS/eip-7917)

#### Mã thực thi Count leading zeros (CLZ) {#count-leading-zeros-opcode}

Tính năng này thêm một lệnh EVM nhỏ, **đếm các số không ở đầu (CLZ)**. Hầu hết mọi thứ trong EVM được biểu diễn dưới dạng giá trị 256-bit—opcode mới này trả về số lượng bit không ở phía trước. Đây là một tính năng phổ biến trong nhiều kiến trúc tập lệnh, vì nó giúp thực hiện các phép toán số học hiệu quả hơn. Trên thực tế, lệnh này gộp những thao tác quét Bit thủ công hiện nay thành một bước duy nhất, nhờ đó việc tìm nhóm Bit, quét Byte hoặc phân tích các trường Bit trở nên đơn giản và rẻ hơn. Các lệnh thực thi này có chi phí cố định thấp và được đo hiệu năng (Benchmarrked) cho thấy tương đương với phép cộng cơ bạn, giúp rút gọn mã Byte và tiết kiệm Gas cho cùng một khối lượng công việc.

**Tài nguyên**: [Thông số kỹ thuật EIP-7939](https://eips.ethereum.org/EIPS/eip-7939)

#### Biên dịch trước để hỗ trợ đường cong secp256r1 {#secp256r1-precompile}

Giới thiệu trình kiểm tra chữ ký secp256r1 (P-256) kiểu khóa mật khẩu tích hợp tại địa chỉ cố định `0x100` sử dụng cùng định dạng lệnh gọi đã được nhiều L2 áp dụng và sửa các trường hợp đặc biệt, do đó các hợp đồng được viết cho các môi trường đó hoạt động trên L1 mà không cần thay đổi.

Nâng cấp UX! Đối với người dùng, điều này mở khóa tính năng ký và khóa mật khẩu gốc của thiết bị. Các ví có thể khai thác trực tiếp Apple Secure Enclave, Android Keystore, các mô-đun bảo mật phần cứng (HSM) và FIDO2/WebAuthn - không cần cụm từ hạt giống, quy trình tham gia mượt mà hơn và các luồng đa yếu tố cho cảm giác như các ứng dụng hiện đại. Điều này mang lại UX tốt hơn, khả năng phục hồi dễ dàng hơn và các mẫu trừu tượng hóa tài khoản phù hợp với những gì hàng tỷ thiết bị đã làm.

Đối với các nhà phát triển, nó nhận đầu vào 160-byte và trả về đầu ra 32-byte, giúp dễ dàng chuyển các thư viện và hợp đồng L2 hiện có. Bên trong, nó bao gồm các kiểm tra điểm-tại-vô-cực và so-sánh-mô-đun để loại bỏ các trường hợp đặc biệt phức tạp mà không làm hỏng các lệnh gọi hợp lệ.

**Tài nguyên**:

- [Thông số kỹ thuật EIP-7951](https://eips.ethereum.org/EIPS/eip-7951)
- [Thông tin thêm về RIP-7212](https://www.alchemy.com/blog/what-is-rip-7212) _(Lưu ý rằng EIP-7951 đã thay thế RIP-7212)_

### Meta {#meta}

#### Phương thức JSON-RPC `eth_config` {#eth-config}

Đây là một lệnh gọi JSON-RPC cho phép bạn hỏi nút của mình về các cài đặt bản fork mà bạn đang chạy. Nó trả về ba ảnh chụp nhanh: `current`, `next`, & `last` để các trình xác thực và công cụ giám sát có thể xác minh rằng các client đã được sắp xếp cho một bản fork sắp tới.

Trên thực tế, điều này nhằm giải quyết một thiếu sót được phát hiện khi bản fork Pectra đi vào hoạt động trên mạng thử nghiệm Holesky vào đầu năm 2025 với các cấu hình sai nhỏ dẫn đến trạng thái không hoàn tất. Điều này giúp các nhóm thử nghiệm và nhà phát triển đảm bảo rằng các bản fork chính sẽ hoạt động như mong đợi khi chuyển từ devnet sang mạng thử nghiệm và từ mạng thử nghiệm sang Mainnet.

Các ảnh chụp nhanh bao gồm: `chainId`, `forkId`, thời gian kích hoạt bản fork đã lên kế hoạch, các biên dịch trước nào đang hoạt động, địa chỉ biên dịch trước, các phụ thuộc hợp đồng hệ thống và lịch trình blob của bản fork.

EIP này nằm trong một phần tách biệt với "Các EIP cốt lõi" vì bản fork không thực sự triển khai bất kỳ thay đổi nào - đó là một thông báo rằng các nhóm client phải triển khai phương thức JSON-RPC này trước bản nâng cấp Fusaka.

**Tài nguyên**: [Thông số kỹ thuật EIP-7910](https://eips.ethereum.org/EIPS/eip-7910)

## Câu hỏi thường gặp {#faq}

### Bản nâng cấp này có ảnh hưởng đến tất cả các nút và trình xác thực Ethereum không? {#does-this-upgrade-affect-all-ethereum-nodes-and-validators}

Đúng, bản nâng cấp Fusaka yêu cầu cập nhật cho cả [Client thực thi và Client đồng thuận](/developers/docs/nodes-and-clients/). Tất cả các ứng dụng khách Ethereum chính sẽ phát hành các phiên bản hỗ trợ đợt phân nhánh cứng được đánh dấu là ưu tiên cao. → Bạn có thể theo dõi thời điểm các bản phát hành này có sẵn trong các Repo Github của Client, [kênh Discord của họ](https://ethstaker.org/support), [Discord của EthStaker](https://dsc.gg/ethstaker), hoặc bằng cách đăng kí theo dõi Blog Ethereum để có thêm cập nhật về giao thức. Để duy trì đồng bộ hóa với mạng Ethereum sau khi nâng cấp, các nhà khai thác nút phải đảm bảo họ đang chạy một phiên bản ứng dụng khách được hỗ trợ. Lưu ý rằng thông tin về các bản phát hành ứng dụng khách có tính nhạy cảm về thời gian và người dùng nên tham khảo các bản cập nhật mới nhất để biết chi tiết hiện tại nhất.

### Làm thế nào để chuyển đổi ETH sau đợt phân nhánh cứng? {#how-can-eth-be-converted-after-the-hardfork}

- **Bạn không cần phải làm gì với ETH của mình**: Sau bản nâng cấp Ethereum Fusaka, bạn không cần phải chuyển đổi hay nâng cấp ETH của mình. Số dư tài khoản của bạn sẽ không thay đổi và ETH bạn đang nắm giữ sẽ vẫn có thể truy cập được ở dạng hiện có sau đợt phân nhánh cứng.
- **Coi chừng Lừa đảo!** <Emoji text="⚠️" /> **bất kỳ ai hướng dẫn bạn "nâng cấp" ETH của mình đều đang cố gắng lừa đảo bạn.** Bạn không cần phải làm gì liên quan đến bản nâng cấp này. Tài sản của bạn sẽ hoàn toàn không bị ảnh hưởng. Hãy nhớ rằng, luôn cập nhật thông tin là cách phòng thủ tốt nhất trước những trò lừa đảo.

[Tìm hiểu thêm về việc nhận biết và tránh các trò lừa đảo](/security/)

### Ngựa vằn có ý nghĩa gì? <Emoji text="🦓" /> {#whats-with-the-zebras}

Ngựa vằn là "linh vật" do nhà phát triển của Fusaka lựa chọn vì các sọc của nó phản ánh việc lấy mẫu tính khả dụng của dữ liệu dựa trên cột của PeerDAS, nơi các nút lưu giữ các mạng con cột nhất định và lấy mẫu một vài cột khác từ mỗi slot của các peer để kiểm tra xem dữ liệu blob có sẵn hay không.

Bản nâng cấp The Merge vào năm 2022 [đã sử dụng gấu trúc](https://x.com/hwwonx/status/1431970802040127498) làm linh vật để báo hiệu sự kết hợp của lớp thực thi & lớp đồng thuận. Kể từ đó, các linh vật đã được chọn một cách không chính thức cho mỗi bản fork và xuất hiện dưới dạng nghệ thuật ASCII trong nhật ký client tại thời điểm nâng cấp. Đó chỉ là một cách thú vị để ăn mừng.

### Những cải tiến nào được bao gồm để mở rộng quy mô L2? {#what-improvements-are-included-for-l2-scaling}

[PeerDAS](/roadmap/fusaka/peerdas) là tính năng chính của bản fork. Nó triển khai lấy mẫu tính khả dụng của dữ liệu (DAS) giúp mở khóa khả năng mở rộng quy mô hơn cho các rollup, về mặt lý thuyết, mở rộng không gian blob lên gấp 8 lần kích thước hiện tại. Thị trường phí blob cũng sẽ được cải thiện để phản ứng hiệu quả với tình trạng tắc nghẽn và đảm bảo các L2 trả một khoản phí hợp lý cho việc tính toán và không gian mà các blob áp đặt lên các nút.

### Các bản fork BPO khác nhau như thế nào? {#how-are-bpo-forks-different}

Các bản fork chỉ tham số blob cung cấp một cơ chế để liên tục tăng số lượng blob (cả mục tiêu và tối đa) sau khi PeerDAS được kích hoạt, mà không cần phải chờ một bản nâng cấp được phối hợp đầy đủ. Mỗi lần tăng đều được mã hóa cứng để được cấu hình sẵn trong các bản phát hành client hỗ trợ Fusaka.

Với tư cách là người dùng hoặc trình xác thực, bạn không cần phải cập nhật client của mình cho mỗi BPO và chỉ cần đảm bảo tuân theo các hardfork chính như Fusaka. Đây là cách làm tương tự như trước đây, không cần hành động đặc biệt nào. Vẫn nên theo dõi các client của bạn xung quanh các bản nâng cấp và BPO và cập nhật chúng ngay cả giữa các bản phát hành chính vì các bản sửa lỗi hoặc tối ưu hóa có thể theo sau hardfork.

### Lịch trình BPO là gì? {#what-is-the-bpo-schedule}

Lịch trình chính xác của các bản cập nhật BPO sẽ được xác định cùng với các bản phát hành Fusaka. Theo dõi [Thông báo giao thức](https://blog.ethereum.org/category/protocol) và ghi chú phát hành của các client của bạn.

Ví dụ về giao diện của nó:

- Trước Fusaka: mục tiêu 6, tối đa 9
- Tại thời điểm kích hoạt Fusaka: mục tiêu 6, tối đa 9
- BPO1, vài tuần sau khi kích hoạt Fusaka: mục tiêu 10, tối đa 15, tăng hai phần ba
- BPO2, vài tuần sau BPO1: mục tiêu 14, tối đa 21

### Điều này có làm giảm phí trên Ethereum (lớp 1) không {#will-this-lower-gas}

Bản nâng cấp này không làm giảm phí gas trên L1, ít nhất là không trực tiếp. Trọng tâm chính là thêm không gian blob cho dữ liệu rollup, do đó làm giảm phí trên lớp 2. Điều này có thể có một số tác dụng phụ đối với thị trường phí L1 nhưng không có thay đổi đáng kể nào được mong đợi.

### Với tư cách là người stake, tôi cần làm gì cho bản nâng cấp? {#as-a-staker-what-do-i-need-to-do-for-the-upgrade}

Như với mọi bản nâng cấp mạng, hãy đảm bảo cập nhật các client của bạn lên các phiên bản mới nhất được đánh dấu hỗ trợ Fusaka. Theo dõi các cập nhật trong danh sách gửi thư và [Thông báo giao thức trên Blog EF](https://blog.ethereum.org/category/protocol) để được thông báo về các bản phát hành.
Để xác thực thiết lập của bạn trước khi Fusaka được kích hoạt trên Mainnet, bạn có thể chạy một trình xác thực trên các mạng thử nghiệm. Fusaka được [kích hoạt sớm hơn trên các mạng thử nghiệm](https://blog.ethereum.org/2025/09/26/fusaka-testnet-announcement) giúp bạn có thêm không gian để đảm bảo mọi thứ hoạt động và báo cáo lỗi. Các bản fork trên mạng thử nghiệm cũng được thông báo trong danh sách gửi thư và blog.

### "Xem trước người đề xuất xác định" (EIP-7917) có ảnh hưởng đến các trình xác thực không? {#does-7917-affect-validators}

Thay đổi này không làm thay đổi cách client trình xác thực của bạn hoạt động, tuy nhiên, nó sẽ cung cấp thêm thông tin chi tiết về các nhiệm vụ trình xác thực của bạn trong tương lai. Hãy đảm bảo cập nhật các công cụ giám sát của bạn để theo kịp các tính năng mới.

### Fusaka ảnh hưởng như thế nào đến yêu cầu băng thông cho các nút và trình xác thực? {#how-does-fusaka-affect-bandwidth-requirements-for-nodes-and-validators}

PeerDAS tạo ra một thay đổi đáng kể trong cách các nút truyền dữ liệu blob. Tất cả dữ liệu được chia thành các phần gọi là cột trên 128 mạng con với các nút chỉ đăng ký một số trong số chúng. Số lượng cột mạng con mà các nút phải lưu giữ phụ thuộc vào cấu hình của chúng và số lượng trình xác thực được kết nối. Yêu cầu băng thông thực tế sẽ phụ thuộc vào số lượng blob được phép trong mạng và loại nút. Tại thời điểm kích hoạt Fusaka, mục tiêu blob vẫn giữ nguyên như trước, nhưng với PeerDAS, các nhà khai thác nút có thể thấy sự sụt giảm trong việc sử dụng đĩa cho các blob và lưu lượng mạng. Khi các BPO cấu hình số lượng blob cao hơn trong mạng, băng thông cần thiết sẽ tăng lên với mỗi BPO.

Các yêu cầu về nút vẫn nằm trong [biên độ khuyến nghị](https://eips.ethereum.org/EIPS/eip-7870) ngay cả sau các BPO của Fusaka.

#### Nút đầy đủ {#full-nodes}

Các nút thông thường không có bất kỳ trình xác thực nào sẽ chỉ đăng ký 4 mạng con, cung cấp dịch vụ lưu giữ 1/8 dữ liệu gốc. Điều này có nghĩa là với cùng một lượng dữ liệu blob, băng thông của nút để tải xuống chúng sẽ nhỏ hơn tám (8) lần. Việc sử dụng đĩa và băng thông tải xuống của các blob cho một nút đầy đủ thông thường có thể giảm khoảng 80%, xuống chỉ còn vài Mb.

#### Người stake một mình {#solo-stakers}

Nếu nút được sử dụng cho một client trình xác thực, nó phải lưu giữ nhiều cột hơn và do đó xử lý nhiều dữ liệu hơn. Khi có thêm trình xác thực, nút sẽ đăng ký ít nhất 8 mạng con cột và do đó xử lý lượng dữ liệu gấp đôi so với nút thông thường nhưng vẫn ít hơn so với trước Fusaka. Nếu số dư của trình xác thực trên 287 ETH, sẽ có ngày càng nhiều mạng con được đăng ký.

Đối với người stake một mình, điều này có nghĩa là việc sử dụng đĩa và băng thông tải xuống của họ sẽ giảm khoảng 50%. Tuy nhiên, để xây dựng các khối cục bộ và tải tất cả các blob lên mạng, cần có nhiều băng thông tải lên hơn. Các nhà xây dựng cục bộ sẽ cần băng thông tải lên cao hơn 2-3 lần so với trước đây tại thời điểm Fusaka và với mục tiêu BPO2 là 15/21 blob, băng thông tải lên cần thiết cuối cùng sẽ phải cao hơn khoảng 5 lần, ở mức 100Mpbs.

#### Các trình xác thực lớn {#large-validators}

Số lượng mạng con đã đăng ký tăng lên khi có thêm số dư và trình xác thực được thêm vào nút. Ví dụ, với số dư khoảng 800 ETH, nút lưu giữ 25 cột và sẽ cần băng thông tải xuống nhiều hơn khoảng 30% so với trước đây. Yêu cầu tải lên tăng tương tự như các nút thông thường và cần ít nhất 100Mbps.

Ở mức 4096 ETH, 2 trình xác thực số dư tối đa, nút sẽ trở thành 'siêu nút' lưu giữ tất cả các cột, do đó tải xuống và lưu trữ mọi thứ. Các nút này chủ động chữa lành mạng bằng cách đóng góp lại dữ liệu bị thiếu nhưng cũng đòi hỏi nhiều băng thông và dung lượng lưu trữ hơn. Với mục tiêu blob cuối cùng cao hơn 6 lần so với trước đây, các siêu nút sẽ phải lưu trữ thêm khoảng 600GB dữ liệu blob và có băng thông tải xuống duy trì nhanh hơn ở khoảng 20Mbps.

[Đọc thêm chi tiết về các yêu cầu dự kiến.](https://ethpandaops.io/posts/fusaka-bandwidth-estimation/#theoretical-requirements)

### Những thay đổi nào của EVM được triển khai? {#what-evm-changes-are-implemented}

Fusaka củng cố EVM với các thay đổi và tính năng nhỏ mới.

- Để đảm bảo an ninh trong khi mở rộng quy mô, kích thước tối đa của một giao dịch sẽ bị [giới hạn ở 16,7 triệu](https://eips.ethereum.org/EIPS/eip-7825) đơn vị gas.
- [Opcode mới đếm các số không ở đầu (CLZ)](https://eips.ethereum.org/EIPS/eip-7939) được thêm vào EVM và sẽ cho phép các ngôn ngữ hợp đồng thông minh thực hiện một số hoạt động nhất định hiệu quả hơn.
- [Chi phí biên dịch trước `ModExp` sẽ tăng lên](https://eips.ethereum.org/EIPS/eip-7883)—các hợp đồng sử dụng nó sẽ tính nhiều gas hơn cho việc thực thi.

### Giới hạn gas 16 triệu mới ảnh hưởng đến các nhà phát triển hợp đồng như thế nào? {#how-does-new-16m-gas-limit-affects-contract-developers}

Fusaka giới thiệu một giới hạn về [kích thước tối đa của một giao dịch là 16,7 triệu](https://eips.ethereum.org/EIPS/eip-7825) (2^24) đơn vị gas. Con số này gần bằng kích thước trước đây của một khối trung bình, đủ lớn để chứa các giao dịch phức tạp có thể tiêu tốn toàn bộ một khối. Giới hạn này tạo ra sự bảo vệ cho các client, ngăn chặn các cuộc tấn công DoS tiềm ẩn trong tương lai với giới hạn gas của khối cao hơn. Mục tiêu của việc mở rộng quy mô là cho phép nhiều giao dịch hơn đi vào chuỗi khối mà không có giao dịch nào tiêu thụ toàn bộ khối.

Các giao dịch thông thường của người dùng còn lâu mới đạt đến giới hạn này. Một số trường hợp đặc biệt như các hoạt động DeFi lớn và phức tạp, triển khai hợp đồng thông minh lớn hoặc các giao dịch hàng loạt nhắm mục tiêu đến nhiều hợp đồng có thể bị ảnh hưởng bởi thay đổi này. Những giao dịch này sẽ phải được chia thành các giao dịch nhỏ hơn hoặc được tối ưu hóa theo cách khác. Sử dụng mô phỏng trước khi gửi các giao dịch có khả năng đạt đến giới hạn.

Phương thức RPC `eth_call` không bị giới hạn và sẽ cho phép mô phỏng các giao dịch lớn hơn giới hạn thực tế của chuỗi khối. Giới hạn thực tế cho các phương thức RPC có thể được cấu hình bởi nhà điều hành client để đảm bảo ngăn chặn lạm dụng.

### CLZ có ý nghĩa gì đối với các nhà phát triển? {#what-clz-means-for-developers}

Các trình biên dịch EVM như Solidity sẽ triển khai và sử dụng chức năng mới để đếm các số không ở bên trong. Các hợp đồng mới có thể được hưởng lợi từ việc tiết kiệm gas nếu chúng dựa vào loại hoạt động này. Theo dõi các bản phát hành và thông báo tính năng của ngôn ngữ hợp đồng thông minh để có tài liệu về các khoản tiết kiệm tiềm năng.

### Có thay đổi nào cho các hợp đồng thông minh hiện có của tôi không? {#what-clz-means-for-developers-2}

Fusaka không có ảnh hưởng trực tiếp nào có thể phá vỡ bất kỳ hợp đồng hiện có nào hoặc thay đổi hành vi của chúng. Các thay đổi được giới thiệu cho lớp thực thi được thực hiện với khả năng tương thích ngược, tuy nhiên, hãy luôn để mắt đến các trường hợp đặc biệt và tác động tiềm tàng.

[Với chi phí biên dịch trước `ModExp` tăng lên](https://eips.ethereum.org/EIPS/eip-7883), các hợp đồng phụ thuộc vào nó sẽ tiêu thụ nhiều gas hơn cho việc thực thi. Nếu hợp đồng của bạn phụ thuộc nhiều vào điều này và trở nên đắt đỏ hơn đối với người dùng, hãy xem xét lại cách nó được sử dụng.

Hãy xem xét [giới hạn 16,7 triệu mới](https://eips.ethereum.org/EIPS/eip-7825) nếu các giao dịch thực thi hợp đồng của bạn có thể đạt đến kích thước tương tự.

## Đọc thêm {#further-reading}

- [Lộ trình Ethereum](/roadmap/)
- [Forkcast: Fusaka](https://forkcast.org/upgrade/fusaka)
- [Fusaka Meta EIP](https://eips.ethereum.org/EIPS/eip-7607)
- [Thông báo trên blog về mạng thử nghiệm Fusaka](https://blog.ethereum.org/2025/09/26/fusaka-testnet-announcement)
- [Bankless: Fusaka & Pectra mang lại gì cho Ethereum](https://www.bankless.com/read/what-fusaka-pectra-will-bring-ethereum)
- [Bankless: Nâng cấp tiếp theo của Ethereum: Fusaka, Glamsterdam & Beyond cùng Preston Van Loon](https://x.com/BanklessHQ/status/1956017743289020633?t=502)
- [Hồ sơ Fusaka](https://www.youtube.com/playlist?list=PL4cwHXAawZxpz-erUbKKUnnGoQNdF8s7Z)
- [Giải thích PEEPanEIPs](https://www.youtube.com/playlist?list=PL4cwHXAawZxoIenfk7OJry4rxcqX-eqBt)
