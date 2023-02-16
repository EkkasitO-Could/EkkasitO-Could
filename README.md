### Hi there 👋

<!--
**EkkasitO-Could/EkkasitO-Could** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

ตลาด การดําเนินการ ตั้งค่า .NET Core SDK
การดําเนินการ GitHub
ตั้งค่า .NET Core SDK
รุ่น 3.0.3
เวอร์ชันล่าสุด
การตั้งค่า dotnet
Basic validation e2e tests

การกระทํานี้ตั้งค่าสภาพแวดล้อม.NET CLI สําหรับใช้ในการดําเนินการโดย:

เลือกดาวน์โหลดและแคชเวอร์ชันของ dotnet ตามเวอร์ชัน SDK และเพิ่มไปยัง PATH
การลงทะเบียนตัวจับคู่ปัญหาสําหรับเอาต์พุตข้อผิดพลาด
การตั้งค่าการตรวจสอบสิทธิ์กับแหล่งแพ็คเกจส่วนตัวเช่นแพ็คเกจ GitHub
โน้ต: นักวิ่งที่โฮสต์ GitHub มี .NET SDK บางเวอร์ชัน ติดตั้งไว้ล่วงหน้า เวอร์ชันที่ติดตั้งอาจมีการเปลี่ยนแปลง โปรดดู เอกสารประกอบ: ซอฟต์แวร์ที่ติดตั้งบน github host runners สําหรับเวอร์ชัน .NET SDK ที่พร้อมใช้งานในปัจจุบัน

การใช้
ดู action.yml

พื้นฐาน:

steps:
- uses: actions/checkout@v3
- uses: actions/setup-dotnet@v3
  with:
    dotnet-version: '3.1.x'
- run: dotnet build <my project>
คำเตือน: เว้นแต่จะมีการระบุเวอร์ชันคอนกรีตในไฟล์ global.json เวอร์ชัน .NET ล่าสุดที่ติดตั้งบน runner (รวมถึงเวอร์ชันที่ติดตั้งไว้ล่วงหน้า) จะถูกใช้ตามค่าเริ่มต้น โปรดดูเอกสารประกอบสําหรับเวอร์ชัน .NET SDK ที่ติดตั้งไว้ล่วงหน้าในปัจจุบัน

การติดตั้งหลายเวอร์ชัน:

steps:
- uses: actions/checkout@v3
- name: Setup dotnet
  uses: actions/setup-dotnet@v3
  with:
    dotnet-version: | 
      3.1.x
      5.0.x
- run: dotnet build <my project>
ไวยากรณ์เวอร์ชันที่รองรับ
อินพุตรองรับไวยากรณ์ต่อไปนี้:dotnet-version

A.B.C (เช่น 6.0.400, 7.0.100-preview.7.22377.5) - ติดตั้งเวอร์ชันที่แน่นอนของ .NET SDK
A.B หรือ A.B.x (เช่น 3.1, 3.1.x) - ติดตั้งเวอร์ชันแพตช์ล่าสุดของ .NET SDK บนช่อง รวมถึงเวอร์ชันก่อนวางจําหน่าย (ตัวอย่าง, rc)3.1
A หรือ A.x (เช่น 3, 3.x) - ติดตั้งแท็กหลักที่ระบุเวอร์ชันรองล่าสุดรวมถึงเวอร์ชันก่อนวางจําหน่าย (ตัวอย่าง, rc)
การใช้อินพุตdotnet-quality
อินพุตนี้ตั้งค่าการดําเนินการเพื่อติดตั้งบิลด์ล่าสุดของคุณภาพที่ระบุในช่อง ค่าที่เป็นไปได้ของคือ: รายวัน, ลงนาม, ตรวจสอบแล้ว, ดูตัวอย่าง, gadotnet-quality

โน้ต: อินพุตสามารถใช้ได้กับเวอร์ชัน .NET SDK ในรูปแบบ 'A.B', 'A.B.x', 'A' และ 'A.x' ที่เวอร์ชันหลักสูงกว่า 5 เท่านั้น ในกรณีอื่น ๆ การป้อนข้อมูลจะถูกละเว้นdotnet-qualitydotnet-quality

steps:
- uses: actions/checkout@v3
- uses: actions/setup-dotnet@v3
  with:
    dotnet-version: '6.0.x'
    dotnet-quality: 'preview'
- run: dotnet build <my project>
การใช้อินพุตglobal-json-file
setup-dotnet การดําเนินการสามารถอ่านเวอร์ชัน .NET SDK จากไฟล์ได้ อินพุตใช้สําหรับระบุเส้นทางไปยัง . หากไม่มีไฟล์ที่ให้มาเพื่อป้อนข้อมูลการดําเนินการจะล้มเหลวโดยมีข้อผิดพลาดglobal.jsonglobal-json-fileglobal.jsonglobal-json-file

โน้ต: ในกรณีที่ใช้ทั้งสองและอินพุตจะมีการติดตั้งเวอร์ชันจากอินพุตทั้งสองdotnet-versionglobal-json-file

steps:
- uses: actions/checkout@v3
- uses: actions/setup-dotnet@v3
  with:
    global-json-file: csharp/global.json
- run: dotnet build <my project>
  working-directory: csharp
การทดสอบเมทริกซ์
การใช้ไวยากรณ์เมทริกซ์เพื่อติดตั้ง .NET SDK หลายเวอร์ชัน:setup-dotnet

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        dotnet: [ '2.1.x', '3.1.x', '5.0.x' ]
    name: Dotnet ${{ matrix.dotnet }} sample
    steps:
      - uses: actions/checkout@v3
      - name: Setup dotnet
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: ${{ matrix.dotnet }}
      - name: Execute dotnet
        run: dotnet build <my project>
โน้ต: เว้นแต่จะมีการระบุเวอร์ชันคอนกรีตในไฟล์ global.json เวอร์ชัน .NET ล่าสุดที่ติดตั้งบน runner (รวมถึงเวอร์ชันที่ติดตั้งไว้ล่วงหน้า) จะถูกใช้ตามค่าเริ่มต้น เมื่อต้องการควบคุมลักษณะการทํางานนี้ คุณอาจต้องการใช้แฟ้มชั่วคราว:global.json

การทดสอบเมทริกซ์ด้วยการสร้าง global.json ชั่วคราว

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        dotnet: [ '2.1.x', '3.1.x', '5.0.x' ]
    name: Dotnet ${{ matrix.dotnet }} sample
    steps:
      - uses: actions/checkout@v3
      - name: Setup dotnet
        uses: actions/setup-dotnet@v3
        id: stepid
        with:
          dotnet-version: ${{ matrix.dotnet }}
      - name: Create temporary global.json
        run: echo '{"sdk":{"version": "${{ steps.stepid.outputs.dotnet-version }}"}}' > ./global.json
      - name: Execute dotnet
        run: dotnet build <my project>
การตั้งค่าการรับรองความถูกต้องสําหรับฟีด nuget
รีจิสทรีแพคเกจ Github (GPR)
steps:
- uses: actions/checkout@v3
- uses: actions/setup-dotnet@v3
  with:
    dotnet-version: '3.1.x'
    source-url: https://nuget.pkg.github.com/<owner>/index.json
  env:
    NUGET_AUTH_TOKEN: ${{secrets.GITHUB_TOKEN}}
- run: dotnet build <my project>
- name: Create the package
  run: dotnet pack --configuration Release <my project>
- name: Publish the package to GPR
  run: dotnet nuget push <my project>/bin/Release/*.nupkg
Azure Artifacts
- uses: actions/setup-dotnet@v3
  with:
    source-url: https://pkgs.dev.azure.com/<your-organization>/_packaging/<your-feed-name>/nuget/v3/index.json
  env:
    NUGET_AUTH_TOKEN: ${{secrets.AZURE_DEVOPS_PAT}} # Note, create a secret with this name in Settings
- name: Publish the package to Azure Artifacts
  run: dotnet nuget push <my project>/bin/Release/*.nupkg
nuget.org
- uses: actions/setup-dotnet@v3
  with:
    dotnet-version: 3.1.x
- name: Publish the package to nuget.org
  run: dotnet nuget push */bin/Release/*.nupkg -k $NUGET_AUTH_TOKEN -s https://api.nuget.org/v3/index.json
  env:
    NUGET_AUTH_TOKEN: ${{ secrets.NUGET_TOKEN }}
โน้ต: เป็นวิธีเดียวที่จะผลักดันแพ็คเกจไปยังฟีด nuget.org สําหรับเครื่อง macOS / Linux เนื่องจากข้อ จํากัด การจัดเก็บการกําหนดค่าคีย์ API

ผลลัพธ์และตัวแปรสภาพแวดล้อม
เอาต์ พุ ต
dotnet-version
การใช้เอาต์พุตเวอร์ชันดอทเน็ตทําให้สามารถติดตั้งโดยแอ็กชัน .NET SDK เวอร์ชันได้

การติดตั้งเวอร์ชันเดียว

ในกรณีของการติดตั้งเวอร์ชันเดียวเอาต์พุตประกอบด้วยเวอร์ชันที่ติดตั้งโดยการกระทําdotnet-version

    - uses: actions/setup-dotnet@v3
      id: stepid
      with:
        dotnet-version: 3.1.422
    - run: echo '${{ steps.stepid.outputs.dotnet-version }}' # outputs 3.1.422
การติดตั้งหลายเวอร์ชัน

ในกรณีที่มีการติดตั้งหลายเวอร์ชันเอาต์พุตประกอบด้วยเวอร์ชันล่าสุดที่ติดตั้งโดยการกระทําdotnet-version

    - uses: actions/setup-dotnet@v3
      id: stepid
      with:
        dotnet-version: | 
          3.1.422
          5.0.408
    - run: echo '${{ steps.stepid.outputs.dotnet-version }}' # outputs 5.0.408
การติดตั้งจาก global.json

เมื่อใช้อินพุตพร้อมกับอินพุตเอาต์พุตจะมีเวอร์ชันที่แก้ไขจาก .dotnet-versionglobal-json-filedotnet-versionglobal.json

    - uses: actions/setup-dotnet@v3
      id: stepid
      with:
        dotnet-version: | 
          3.1.422
          5.0.408
        global-json-file: "./global.json" # contains version 2.2.207
    - run: echo '${{ steps.stepid.outputs.dotnet-version }}' # outputs 2.2.207
ตัวแปรสภาพแวดล้อม
ตัวแปรสภาพแวดล้อมบางอย่างอาจจําเป็นสําหรับกรณีเฉพาะของคุณหรือเพื่อปรับปรุงการบันทึก ตัวอย่างบางส่วนแสดงอยู่ด้านล่าง แต่รายการทั้งหมดพร้อมรายละเอียดทั้งหมดสามารถพบได้ที่นี่: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-environment-variables

com.Env.variable	การบรรยาย	ค่าเริ่มต้น
DOTNET_INSTALL_DIR	ระบุไดเร็กทอรีที่ควรติดตั้ง .NET SDK โดยการดําเนินการ	ค่าเริ่มต้นสําหรับแต่ละระบบปฏิบัติการ
DOTNET_NOLOGO	ลบโลโก้และข้อความ telemetry ออกจากการเรียกใช้ครั้งแรกของ dotnet cli	ปลอม
DOTNET_CLI_TELEMETRY_OPTOUT	การเลือกไม่ใช้การวัดและส่งข้อมูลทางไกลไปยัง Microsoft	ปลอม
DOTNET_MULTILEVEL_LOOKUP	กําหนดค่าว่าตําแหน่งการติดตั้งส่วนกลางถูกใช้เป็นสํารองหรือไม่	จริง
ค่าเริ่มต้นของตัวแปรสภาพแวดล้อมขึ้นอยู่กับระบบปฏิบัติการที่ใช้กับนักวิ่ง:DOTNET_INSTALL_DIR

ระบบปฏิบัติการ	ค่าเริ่มต้น
หน้าต่าง	C:\Program Files\dotnet
อูบุนตู	/usr/share/dotnet
macOS	/Users/runner/.dotnet
ตัวอย่างการใช้งาน:

build:
  runs-on: ubuntu-latest
  env:
    DOTNET_INSTALL_DIR: "path/to/directory"
  steps:
    - uses: actions/checkout@main
    - uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '3.1.x'
ใบอนุญาต
สคริปต์และเอกสารในโครงการนี้ได้รับการเผยแพร่ภายใต้ใบอนุญาต MIT

ผลงาน
ยินดีต้อนรับการมีส่วนร่วม! ดูคู่มือผู้ร่วมให้ข้อมูล

 ผู้สร้างที่ได้รับการยืนยัน
GitHub ได้ตรวจสอบแล้วว่าการกระทํานี้สร้างขึ้นโดยการกระทํา

ดูข้อมูลเพิ่มเติมเกี่ยวกับการดําเนินการที่ยืนยันแล้ว

ดาว
