# 관계장부 제3자 구성요소 고지

이 문서는 관계장부 배포 고지입니다. 실제 포함 패키지는 manifest.json의 runtimePackages와 bundle-meta.json에 기록합니다. 라이선스 전문은 licenses/와 단일 설치 JS의 첫 주석에 함께 들어갑니다.

## 실행 라이브러리

| 구성요소 | 버전 | 라이선스 | 출처 |
|---|---|---|---|
| pdf-lib | 1.17.1 | MIT | https://github.com/Hopding/pdf-lib |
| @pdf-lib/fontkit | 1.1.1 | MIT 및 사전 번들 고지 | https://github.com/Hopding/fontkit |
| pako | 1.0.11 | MIT AND Zlib | https://github.com/nodeca/pako |
| @pdf-lib/standard-fonts | 1.0.0 | MIT | https://github.com/Hopding/standard-fonts |
| @pdf-lib/upng | 1.0.1 | MIT | https://github.com/Hopding/upng |
| tslib | 1.14.1 | 0BSD | https://github.com/microsoft/tslib |

버전과 무결성 값은 package-lock.json으로 고정합니다. 라이브러리는 번들·축소되므로 원래 배포 파일과 동일한 파일이라고 표시하지 않습니다. 원래 구현을 관계장부 작성물이라고 주장하지 않습니다.

fontkit npm 1.1.1에는 별도 LICENSE 파일이 없고 package.json의 MIT 표시와 README의 MIT 링크가 있습니다. package.json은 Andrew Dillon을 author, Devon Govett를 contributor로 명시합니다. 아래 MIT 전문은 그 표시를 위한 사본입니다. 사전 번들 소스의 Joyent/Node 기여자, Niklas von Hertzen의 MIT 고지와 Google Inc.의 Apache-2.0 고지를 fontkit-bundled-NOTICES.txt에 보존합니다. 사전 번들 내부 의존성의 개별 버전은 추정하지 않습니다.

Google Brotli 코드의 Apache-2.0 전문도 제공합니다. pako의 최상위 MIT 파일 외에 lib/zlib/deflate.js에 있는 Zlib 저작권·사용 조건을 보존합니다. tslib는 MIT가 아니라 0BSD입니다.

## 내장 글꼴

| 원본 | 고정 커밋 | 변형 이름 | 라이선스 |
|---|---|---|---|
| Noto Sans KR | 4efc2774c63917927efe769ca845def6bd6debae | Relation Ledger KR | SIL OFL 1.1 |
| Noto Emoji | b979dba422e445492b0eb9951ac52ee0b4d648c3 | Relation Ledger Emoji | SIL OFL 1.1 |
| Noto Sans Symbols 2 | 7b6724ac7ececc713e9ba93af309f7520c9a80a3 | Relation Ledger Symbols | SIL OFL 1.1 |
| Noto Sans SC | a85815a42757630ce188fdad368c2dfc444d4773 | Relation Ledger CJK Fallback | SIL OFL 1.1 |

원본 출처는 Google Fonts 공식 저장소입니다.

- https://github.com/google/fonts/blob/4efc2774c63917927efe769ca845def6bd6debae/ofl/notosanskr/NotoSansKR%5Bwght%5D.ttf
- https://github.com/google/fonts/blob/b979dba422e445492b0eb9951ac52ee0b4d648c3/ofl/notoemoji/NotoEmoji%5Bwght%5D.ttf
- https://github.com/google/fonts/blob/7b6724ac7ececc713e9ba93af309f7520c9a80a3/ofl/notosanssymbols2/NotoSansSymbols2-Regular.ttf
- https://github.com/google/fonts/blob/a85815a42757630ce188fdad368c2dfc444d4773/ofl/notosanssc/NotoSansSC%5Bwght%5D.ttf

저작권과 OFL 전문은 licenses/NotoSansKR-TTF-OFL.txt, licenses/NotoEmoji-OFL.txt, licenses/NotoSansSymbols2-OFL.txt, licenses/NotoSansSC-OFL.txt에 보존합니다. font-manifest.json에는 원본·변형본의 SHA256, 크기, 문자 수가 있습니다.

beta.19의 CJK 보조 글꼴은 앞선 내장 글꼴에 없는 Unicode 매핑만 보존한 변형본입니다. 각 Unicode 문자에 서로 다른 글리프 ID를 주기 위해 같은 윤곽·폭을 가진 별칭을 복제하며, 문자 코드 자체를 비슷한 문자로 치환하지 않습니다. 범위·NFC 정규화의 제한은 assets/PROVENANCE.md에 기록합니다.

변형본은 regular 400 고정 굵기로 만들고 이름을 바꿨습니다. 한글 글꼴은 힌팅과 사용하지 않는 레이아웃 변형을 제거하되 전체 Unicode 매핑과 ccmp/ liga를 유지합니다. 모든 glyf를 4바이트 경계에 맞춰 작은 서브셋에서 홀수 loca 오프셋이 잘리지 않도록 했습니다. gzip/base64는 JS 안에 포함되고, PDF에는 사용한 글리프의 서브셋만 들어갑니다. Emoji는 단색 윤곽입니다. 미사용 Nanum/CFF/WOFF2 실험 파일은 배포 대상이 아닙니다.

## 개발 도구와 사용자 자료

esbuild 0.25.12는 빌드 전용입니다. fonttools 4.59.2와 brotli 1.1.0은 글꼴 재생성 전용이며 설치 JS에 들어가지 않습니다. 기존 PDF Pod 코드는 복사하지 않고 조사한 포장 동작을 새로 구현했습니다.

cocoA 가져오기 프리셋은 사용자가 보유한 지침·스킬을 변환한 자료입니다. 원래 자료의 권리·배포 조건은 그 작성자에게 있으며 이 고지가 별도 재배포 허가를 부여하지 않습니다.

## fontkit MIT 라이선스 사본

<!-- LICENSE:fontkit-MIT -->
MIT License

Attribution: Andrew Dillon and Devon Govett; see @pdf-lib/fontkit 1.1.1 package.json author/contributors and MIT license declaration.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
<!-- END_LICENSE:fontkit-MIT -->

## Apache License 2.0

Source: https://www.apache.org/licenses/LICENSE-2.0.txt

<!-- LICENSE:Apache-2.0 -->

                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS

   APPENDIX: How to apply the Apache License to your work.

      To apply the Apache License to your work, attach the following
      boilerplate notice, with the fields enclosed by brackets "[]"
      replaced with your own identifying information. (Don't include
      the brackets!)  The text should be enclosed in the appropriate
      comment syntax for the file format. We also recommend that a
      file or class name and description of purpose be included on the
      same "printed page" as the copyright notice for easier
      identification within third-party archives.

   Copyright [yyyy] [name of copyright owner]

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

<!-- END_LICENSE:Apache-2.0 -->
