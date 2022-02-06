---
title: Triển khai giải pháp NFTs Marketplace trên hạ tầng AWS siêu nhanh
date: 2022-02-06T02:27:02.831Z
image: /images/shubham-dhage-jlijbotswuw-unsplash-1-.jpg
draft: true
---
<!--StartFragment-->

## Bối cảnh

Để hòa mình cùng phong trào Cách mạng Công nghiệp lần thứ tư (tiếng Tây kêu bằng: The Fourth Industrial Revolution, 4IR, or Industry 4.0) và sự chuyển mình của Thế giới cũng như đề cao tinh thần đi tắt đón đầu, đi sau về trước và nhanh chóng ~~lùa gà~~ phổ cập NFTs để đưa nước ta sánh vai cùng các cường quốc năm châu.

Từ những lý do cấp thiết trên, tui đã quyết định tìm giải pháp nhanh để triển khai nhanh NFTs Marketplace trên hạ tầng AWS, sau khi vọc xong thấy đúng là nhanh thật, thậm chí còn siêu nhanh nữa.

<!-- excerpt -->

Sở dĩ lựa AWS (hay các cloud provider khác cũng thế) là tại vì mấy người không biết gì như tui giờ già cả rồi thời gian nghiên cứu không còn nhiều, sức khỏe thì yếu không khiêng nổi mấy con server 4U 8U nhét vô rack cao hơn đầu người rồi lọ mọ cả buổi trong cái phòng có mười mấy độ với độ ẩm 50% nổi nữa, thành ra cứ lên mây cho sướng. Thiên hạ hay nói ba cái chuyện mây mưa sướng lắm, thật là sướng thật!

OK, vậy chúng ta sẽ xài Ethereum Ropsten Testnet với sự giúp sức đắc lực của Amazon Managed Blockchain cùng với lủ khủ một mớ mấy cái services khác phụ họa như hình minh họa bên dưới. Tất cả những services này đều được khởi tạo bằng CloudFormation.

[![](https://raudangdat.files.wordpress.com/2022/01/nft-marketplace-aws-architecture.png?w=821)](https://raudangdat.files.wordpress.com/2022/01/nft-marketplace-aws-architecture.png)

Hình của AWS Sample.

## Bắt đầu

Kiểm tra phiên bản Nodejs, mấy phiên bản cũ quá không còn support hay gặp nhiều lỗi trời ơi đất hỡi lắm. Trên Ubuntu mặc định cài vô là bản 10.x, thành ra phải update hoặc lúc cài mới nhớ chú ý theo hướng dẫn này: [](https://thocode.net/blog/cai-dat-node-js-phien-ban-moi-nhat-tren-ubuntu-wsl2/)<https://thocode.net/blog/cai-dat-node-js-phien-ban-moi-nhat-tren-ubuntu-wsl2/>

[![](https://raudangdat.files.wordpress.com/2022/01/cdk-nodejs-unsupport-version.png?w=1024)](https://raudangdat.files.wordpress.com/2022/01/cdk-nodejs-unsupport-version.png)

CDK không chạy được với các phiên bản Nodejs cũ.

Clone source và install dependencies

`git clone https://github.com/aws-samples/simple-nft-marketplace.git`

`npm install`

## Deploy Contract

Mình sẽ xài hardhat để deploy contract ERC721 viết bằng Solidity lên Ethereum Ropsten Testnet. Coi thêm ở [](https://hardhat.org/)<https://hardhat.org/> nếu bạn quan tâm, cơ bản thì hardhat là môi trường phát triển của Ethereum, cũng như muốn code Java thì phải JDK hay làm .NET thì phải có .NET Framework hay .NET SDK vậy.

Chạy lệnh trong thư mục /contract

`npm install`

`npx hardhat compile`

### Chạy thử trên localhost

Mở 2 terminal để giả bộ rằng một cái là server, còn cái kia là client tương tác với server.

* Cái đầu, chạy lệnh:

`npx hardhat node`

Thấy hiện ra 20 cái Account và Private Key mỗi cái 10000 ETH là được, phải chi cái này đồ thiệt thì đã ha, tới đây nghỉ hưu được rồi rồi cần chi ~~lùa gà~~ mần mướn nữa. Nếu cần nhìn trực quan thì có thể dùng ví nào đó như MataMask/ Trust Wallet/ Phantom mở testnet network lên, chọn [Localhost](http://localhost/) 8545 rồi import account test vô.

`Account #0: 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 (10000 ETH) Private Key: 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80`

* Chuyển qua cái terminal 2, chạy:

`npx hardhat console --network localhost`

Thấy hiện ra vầy là OK:

`Contract deployed at 0x5FbDB2315678afecb367f032d93F642f64180aa3`

Tiếp tục chạy lệnh này để mở hardhat console thực hiện việc sinh ra NFT token bằng SimpleERC721 nằm trong contract/contracts/SimpleERC721.sol

`npx hardhat console --network localhost`

Trong hardhat console chạy lần lượt, nhớ thay thế <> bằng address vừa hiện ra ở bên trên.

```

```

Thấy vầy là OK:

[![](https://raudangdat.files.wordpress.com/2022/01/hardhat-contract-deploy.png?w=1011)](https://raudangdat.files.wordpress.com/2022/01/hardhat-contract-deploy.png)

Quay lại MetaMask sẽ thấy đã tốn:

[![](https://raudangdat.files.wordpress.com/2022/01/metamask-localhost8545.png?w=432)](https://raudangdat.files.wordpress.com/2022/01/metamask-localhost8545.png)

Nếu nhìn trên terminal 1 (server) cũng sẽ thấy các thông tin thế này

[![](https://raudangdat.files.wordpress.com/2022/01/hardhat-server-terminal.png?w=1024)](https://raudangdat.files.wordpress.com/2022/01/hardhat-server-terminal.png)

### Chạy thử trên Ethereum Ropsten Testnet

Đăng nhập vô AWS Console > Managed Blockchain > Networks > Ethereum Testnet Ropsten > tạo một node > copy HTTP Endpoint để thế vô lệnh này. Hết sức chú ý là phải có https nữa nha, tui gặp lỗi mò đã đời mới biết.

`export AMB_HTTP_ENDPOINT='<my-endpoint>'`

Tiếp tục tạo account để phục vụ cho việc deploy contract, đại khái acc này như là 20 acc có sẵn 10K ETH ở trên vậy nhưng có điều mới tạo thì không có đồng ETH nào nên muốn trả phí gas khi deploy thì giờ phải đi kiếm mấy cái Ropsten Faucet để gửi ít rETH vào ví. Cứ Google, nhiều trang làm được việc này, có trang thì dễ, có trang thì bắt phải giải captcha mới gửi cho.

`npx hardhat account`

Lấy thông tin vừa chạy ở trên bỏ vô đây

`export PRIVATE_KEY='<0x...>'`

Tiếp đến quay lại AWS Console vào Identity and Access Management (IAM) để tạo access key và scret access key. Chú ý là IAM bản cũ, chứ IAMv2 thì click nút Manage access keys để nó qua bản cũ nhe. Có thông tin thì điền vô đây:

`export AWS_ACCESS_KEY_ID='<...>' export AWS_SECRET_ACCESS_KEY='<...>'`

Chạy lệnh này để deploy với Amazon Managed Blockchain. (1).`npx hardhat run --network amb scripts/deploy-amb.js`

Vì thư viện @aws\web3-http-provider\index.js đang để mặc định là us-east-1 nên nếu đang ở region khác sẽ gặp lỗi, cần phải set lại như bên dưới. Xong thì chạy lại file deploy-amb.js ở trên là được, thành công sẽ gặp dòng “Contract deployed at” và bị trừ tiền gas.

`export AWS_DEFAULT_REGION='<your-region>'`

## 3. Deploy API cho Backend

Cài đặt AWS CDK

`npm install -g aws-cdk`

Các lệnh bên dưới sẽ chạy trong thư mục /provision

`npm install`

`export CONTRACT_ADDRESS='<contract ở (1)>'`

`cdk bootstrap`

Chạy lệnh trên thì thằng CloudFormation sẽ tạo 1 stack là CDKToolkit để chuẩn bị cho việc deploy.

![✅](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/2705.svg) Environment aws://\*\**/ap-southeast-1 bootstrapped.

Chạy 3 lệnh này để vào-install dependencies-quay lại:

`cd lambda; npm install; cd -;`

Copy complied contract (SimpleERC721.json) vào /lambda/contracts/

`cp ../contract/artifacts/contracts/SimpleERC721.sol/SimpleERC721.json lambda/contracts/.`

Build CDK

`npm run build`

Check lại coi mấy biến môi trường set đúng chưa

`echo $AMB_HTTP_ENDPOINT`

`echo $CONTRACT_ADDRESS`

OK thì deploy, CloudFormation tiếp tục tạo stack SimpleNftMarketplaceStack.

`cdk deploy SimpleNftMarketplaceStack`

Như đã nói ngay khúc mở đầu, không chịu update Nodejs lên đúng phiên bản CDK được hỗ trợ nên gặp đủ thứ lỗi trời ơi đất hỡi ngay khúc giữa không, mà lúc đó lỡ làm rồi nên lại làm biếng làm lại từ đầu ![😂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f602.svg)

Số là đoạn này tui gặp lỗi vầy từ chiều, xong tui mò hoài không ra nên thôi tui đi ún gụ. Sau khi sin sỉn về vì chưa bù ngủ nên thôi tui mở máy lên tiếp rồi gõ tùm lum gì đó trong ba bốn cái terminal vừa mở ra, giờ chả nhớ đã gõ cái gì, vẫn không chạy được, thế là copy error log Google đại thì thấy trên Stackoverflow có ông nào đó trả lời về cái lỗi này cách đây 3 năm trước dù rằng nhìn đề bài thì có vẻ tay hỏi đang xài electron-builder gì đó, chưa kịp suy nghĩ coi có đúng cái mình cần không nữa, tui copy và paste vô đại, ai dè hết thấy lỗi, xong cái chạy CDK Deploy enter một phát được như là các thánh IT trong những đền thờ các huyền thoại vậy.

Trời đất quỷ thần thiên địa ơi, ghê vậy trời! ![🤣](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f923.svg)

Nói chứ, lỗi vầy thì đúng là liên quan đến cục electron rồi.

`Error: EACCES: permission denied, stat '/root/.cache/electron/8c5c987a73913c5646db497de9f6f9676033aa1586938d0d2c9cac8ac37f7e20/electron-v15.3.2-linux-x64.zip'`

Vậy nên coi ở đây [](https://stackoverflow.com/questions/51469367/electron-builder-eacces-permission-denied)<https://stackoverflow.com/questions/51469367/electron-builder-eacces-permission-denied> rồi cọp 2 lệnh này chạy, xong chạy lại cái cdk deploy là OK. Tuyệt vời phải không nào, cảm ơn Internet, cảm ơn ai đã mang Stackoverflow đến với thế giới loài người.

`sudo npm uninstall -g electron`

`sudo npm install -g electron --unsafe-perm=true --allow-root`

Sau khi chạy thành công thì sẽ có Output thế này `SimpleNftMarketplaceStack.NftApiEndpoint = https://***.execute-api.ap-southeast-1.amazonaws.com/prod/ SimpleNftMarketplaceStack.NftApiEndpoint8C6C6AD5 = https://***.execute-api.ap-southeast-1.amazonaws.com/prod/ SimpleNftMarketplaceStack.UserPoolClientId = *** SimpleNftMarketplaceStack.UserPoolId = ap-southeast-1*** Stack ARN: arn:aws:cloudformation:ap-southeast-1:***:stack/SimpleNftMarketplaceStack/***`

# 4. Frontend

Phần này nằm trong thư mục /marketplace.

Chuyển vô thư mục /marketplace rồi set các biến môi trường như bên dưới.

|     |     |
| --- | --- |
|     |     |

Nhớ thay giá trị Output ở phần Deploy API vô mấy cái biến ở trên, để ý bỏ hai dấu < > luôn nhe. <region> The region you deployed your stack in previous steps <api-endpoint> NftApiEndpoint output from Deploy API <user-pool> UserPoolId output from Deploy API <web-client> UserPoolClientId output from Deploy API

`sudo npm install`

Không hiểu mình chạy thì lỗi “npm ERR! Response timeout while trying to fetch [](https://registry.npmjs.org/fs-extra)<https://registry.npmjs.org/fs-extra> (over 30000ms)” nên phải

`npm set timeout=100000`

Sau đó thì phải chạy lệnh dưới để cho sạch chứ không thì lỗi “Unexpected end of JSON input while parsing near” nhìn rất là huyền bí.

`npm cache clean --force`

Giờ thì chạy OK rồi đó, hơi chậm. Chạy tiếp cái này

`sudo npm run serve`

Trường hợp lỗi liên quan đến vue-cli-service thì cài thêm dependence rồi chạy lại npm run serve.

`npm i @vue/cli-service`

Thấy báo địa chỉ Local với Network là OK, lấy browser mở ra vầy là coi như OK lần 2.

[![](https://raudangdat.files.wordpress.com/2022/01/nft-marketplace-frontend.png?w=650)](https://raudangdat.files.wordpress.com/2022/01/nft-marketplace-frontend.png)

Photo by [Shubham Dhage](https://unsplash.com/@theshubhamdhage?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/blockchain?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)



<!--EndFragment-->