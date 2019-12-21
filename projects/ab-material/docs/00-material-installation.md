Project         : JAGO 
Version         : aa-material 00.01
Build           : 00-material-installation
Document        : 00-material-installation.md
Start           : Jum'at, 20 Desember 2019 02:31
End             : Jum'at, 21 Desember 2019 05:10

Task            : Build a new subversion for seed with Google Material and ready for 
                  exercises medium of material implementation.
                  
Ada beberapa UI packages yang dibangun untuk Google Angular. Walaupun tidak selengkap yang lain, ditetapkan package dari Google Material sebagai packages yang akan menangani hampir seluruh kebutuhan User Interface dalam JAGO projects. Penggunaan independent package untuk beberapa element UI diijinkan untuk diterapkan.

## New Subversion

0. Generate

  ```bash
  $ ng generate application ab-material --inlineStyle=false --inlineTemplate=false --prefix=emd --style=scss
  ? Would you like to add Angular routing? No
  CREATE projects/ab-material/browserslist (429 bytes)
  CREATE projects/ab-material/karma.conf.js (1027 bytes)
  CREATE projects/ab-material/tsconfig.app.json (278 bytes)
  CREATE projects/ab-material/tsconfig.spec.json (278 bytes)
  CREATE projects/ab-material/tslint.json (247 bytes)
  CREATE projects/ab-material/src/favicon.ico (948 bytes)
  CREATE projects/ab-material/src/index.html (296 bytes)
  CREATE projects/ab-material/src/main.ts (372 bytes)
  CREATE projects/ab-material/src/polyfills.ts (2838 bytes)
  CREATE projects/ab-material/src/styles.scss (80 bytes)
  CREATE projects/ab-material/src/test.ts (642 bytes)
  CREATE projects/ab-material/src/assets/.gitkeep (0 bytes)
  CREATE projects/ab-material/src/environments/environment.prod.ts (51 bytes)
  CREATE projects/ab-material/src/environments/environment.ts (662 bytes)
  CREATE projects/ab-material/src/app/app.module.ts (314 bytes)
  CREATE projects/ab-material/src/app/app.component.scss (0 bytes)
  CREATE projects/ab-material/src/app/app.component.html (25498 bytes)
  CREATE projects/ab-material/src/app/app.component.spec.ts (996 bytes)
  CREATE projects/ab-material/src/app/app.component.ts (216 bytes)
  CREATE projects/ab-material/e2e/protractor.conf.js (808 bytes)
  CREATE projects/ab-material/e2e/tsconfig.json (226 bytes)
  CREATE projects/ab-material/e2e/src/app.e2e-spec.ts (644 bytes)
  CREATE projects/ab-material/e2e/src/app.po.ts (262 bytes)
  UPDATE angular.json (8075 bytes)
  UPDATE package.json (1414 bytes)
  npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.11 (node_modules/fsevents):
  npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.11: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

  added 1 package from 1 contributor, removed 1 package, updated 1 package and audited 20965 packages in 27.997s

  21 packages are looking for funding
    run `npm fund` for details

  found 2 moderate severity vulnerabilities
    run `npm audit fix` to fix them, or `npm audit` for details
  ```

1. Resolves vulnerabilities

  ```bash
  $ npx npm-force-resolutions
  npx: installed 5 in 6.174s

  $ npm update
  npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.

  > @angular/cli@8.3.21 postinstall /home/wandyatmono/projects/jago/frontend/node_modules/@angular/cli
  > node ./bin/postinstall/script.js

  npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.11 (node_modules/fsevents):
  npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.11: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

  + @angular-devkit/build-angular@0.803.21
  + @angular/cli@8.3.21
  added 8 packages from 7 contributors, removed 20 packages, updated 22 packages, moved 1 package and audited 20968 packages in 67.203s

  5 packages are looking for funding
    run `npm fund` for details

  found 0 vulnerabilities
  ```

2. Perubahan pada `angular.json`

  ```json
  {
    "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
    "version": 1,
    "newProjectRoot": "projects",
    "projects": {
      "aa-seed": {
        "projectType": "application",
        "schematics": {
          "@schematics/angular:component": {
            "style": "scss"
          }
        },
        "root": "projects/aa-seed",
        "sourceRoot": "projects/aa-seed/src",
        "prefix": "emd",
        "architect": {
          "build": {
            "builder": "@angular-devkit/build-angular:browser",
            "options": {
              "outputPath": "dist/aa-seed",
              "index": "projects/aa-seed/src/index.html",
              "main": "projects/aa-seed/src/main.ts",
              "polyfills": "projects/aa-seed/src/polyfills.ts",
              "tsConfig": "projects/aa-seed/tsconfig.app.json",
              "aot": false,
              "assets": [
                "projects/aa-seed/src/favicon.ico",
                "projects/aa-seed/src/assets"
              ],
              "styles": [
                "./node_modules/@angular/material/prebuilt-themes/indigo-pink.css",
                "projects/aa-seed/src/styles.scss"
              ],
              "scripts": []
            },
            "configurations": {
              "production": {
                "fileReplacements": [
                  {
                    "replace": "projects/aa-seed/src/environments/environment.ts",
                    "with": "projects/aa-seed/src/environments/environment.prod.ts"
                  }
                ],
                "optimization": true,
                "outputHashing": "all",
                "sourceMap": false,
                "extractCss": true,
                "namedChunks": false,
                "aot": true,
                "extractLicenses": true,
                "vendorChunk": false,
                "buildOptimizer": true,
                "budgets": [
                  {
                    "type": "initial",
                    "maximumWarning": "2mb",
                    "maximumError": "5mb"
                  },
                  {
                    "type": "anyComponentStyle",
                    "maximumWarning": "6kb",
                    "maximumError": "10kb"
                  }
                ]
              }
            }
          },
          "serve": {
            "builder": "@angular-devkit/build-angular:dev-server",
            "options": {
              "browserTarget": "aa-seed:build"
            },
            "configurations": {
              "production": {
                "browserTarget": "aa-seed:build:production"
              }
            }
          },
          "extract-i18n": {
            "builder": "@angular-devkit/build-angular:extract-i18n",
            "options": {
              "browserTarget": "aa-seed:build"
            }
          },
          "test": {
            "builder": "@angular-devkit/build-angular:karma",
            "options": {
              "main": "projects/aa-seed/src/test.ts",
              "polyfills": "projects/aa-seed/src/polyfills.ts",
              "tsConfig": "projects/aa-seed/tsconfig.spec.json",
              "karmaConfig": "projects/aa-seed/karma.conf.js",
              "assets": [
                "projects/aa-seed/src/favicon.ico",
                "projects/aa-seed/src/assets"
              ],
              "styles": [
                "./node_modules/@angular/material/prebuilt-themes/indigo-pink.css",
                "projects/aa-seed/src/styles.scss"
              ],
              "scripts": []
            }
          },
          "lint": {
            "builder": "@angular-devkit/build-angular:tslint",
            "options": {
              "tsConfig": [
                "projects/aa-seed/tsconfig.app.json",
                "projects/aa-seed/tsconfig.spec.json",
                "projects/aa-seed/e2e/tsconfig.json"
              ],
              "exclude": [
                "**/node_modules/**"
              ]
            }
          },
          "e2e": {
            "builder": "@angular-devkit/build-angular:protractor",
            "options": {
              "protractorConfig": "projects/aa-seed/e2e/protractor.conf.js",
              "devServerTarget": "aa-seed:serve"
            },
            "configurations": {
              "production": {
                "devServerTarget": "aa-seed:serve:production"
              }
            }
          }
        }
      },
      "ab-material": {
        "projectType": "application",
        "schematics": {
          "@schematics/angular:component": {
            "style": "scss"
          }
        },
        "root": "projects/ab-material",
        "sourceRoot": "projects/ab-material/src",
        "prefix": "emd",
        "architect": {
          "build": {
            "builder": "@angular-devkit/build-angular:browser",
            "options": {
              "outputPath": "dist/ab-material",
              "index": "projects/ab-material/src/index.html",
              "main": "projects/ab-material/src/main.ts",
              "polyfills": "projects/ab-material/src/polyfills.ts",
              "tsConfig": "projects/ab-material/tsconfig.app.json",
              "aot": false,
              "assets": [
                "projects/ab-material/src/favicon.ico",
                "projects/ab-material/src/assets"
              ],
              "styles": [
                "projects/ab-material/src/styles.scss"
              ],
              "scripts": []
            },
            "configurations": {
              "production": {
                "fileReplacements": [
                  {
                    "replace": "projects/ab-material/src/environments/environment.ts",
                    "with": "projects/ab-material/src/environments/environment.prod.ts"
                  }
                ],
                "optimization": true,
                "outputHashing": "all",
                "sourceMap": false,
                "extractCss": true,
                "namedChunks": false,
                "aot": true,
                "extractLicenses": true,
                "vendorChunk": false,
                "buildOptimizer": true,
                "budgets": [
                  {
                    "type": "initial",
                    "maximumWarning": "2mb",
                    "maximumError": "5mb"
                  },
                  {
                    "type": "anyComponentStyle",
                    "maximumWarning": "6kb",
                    "maximumError": "10kb"
                  }
                ]
              }
            }
          },
          "serve": {
            "builder": "@angular-devkit/build-angular:dev-server",
            "options": {
              "browserTarget": "ab-material:build"
            },
            "configurations": {
              "production": {
                "browserTarget": "ab-material:build:production"
              }
            }
          },
          "extract-i18n": {
            "builder": "@angular-devkit/build-angular:extract-i18n",
            "options": {
              "browserTarget": "ab-material:build"
            }
          },
          "test": {
            "builder": "@angular-devkit/build-angular:karma",
            "options": {
              "main": "projects/ab-material/src/test.ts",
              "polyfills": "projects/ab-material/src/polyfills.ts",
              "tsConfig": "projects/ab-material/tsconfig.spec.json",
              "karmaConfig": "projects/ab-material/karma.conf.js",
              "assets": [
                "projects/ab-material/src/favicon.ico",
                "projects/ab-material/src/assets"
              ],
              "styles": [
                "projects/ab-material/src/styles.scss"
              ],
              "scripts": []
            }
          },
          "lint": {
            "builder": "@angular-devkit/build-angular:tslint",
            "options": {
              "tsConfig": [
                "projects/ab-material/tsconfig.app.json",
                "projects/ab-material/tsconfig.spec.json",
                "projects/ab-material/e2e/tsconfig.json"
              ],
              "exclude": [
                "**/node_modules/**"
              ]
            }
          },
          "e2e": {
            "builder": "@angular-devkit/build-angular:protractor",
            "options": {
              "protractorConfig": "projects/ab-material/e2e/protractor.conf.js",
              "devServerTarget": "ab-material:serve"
            },
            "configurations": {
              "production": {
                "devServerTarget": "ab-material:serve:production"
              }
            }
          }
        }
      }
    },
    "defaultProject": "aa-seed"
  }
  ```

## Google Material Installation

Sumber: https://material.angular.io/guide/getting-started

0. Installation

  ```bash
  $ ng add @angular/material
  ```

  Hasil:

  ```bash
  Installing packages for tooling via npm.
  Installed packages for tooling via npm.
  ? Choose a prebuilt theme name, or "custom" for a custom theme: Indigo/Pink        [ Preview: https://material.angular.io?theme=indigo-pink ]
  ? Set up HammerJS for gesture recognition? Yes
  ? Set up browser animations for Angular Material? Yes
  UPDATE package.json (1504 bytes)
  npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.11 (node_modules/fsevents):
  npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.11: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

  added 3 packages from 4 contributors and audited 20974 packages in 28.381s

  23 packages are looking for funding
    run `npm fund` for details

  found 0 vulnerabilities

  UPDATE projects/aa-seed/src/main.ts (391 bytes)
  UPDATE projects/aa-seed/src/app/app.module.ts (423 bytes)
  UPDATE angular.json (8242 bytes)
  UPDATE projects/aa-seed/src/index.html (486 bytes)
  UPDATE projects/aa-seed/src/styles.scss (181 bytes)
  ```

  > CATATAN: theme dipilih `indigo/pink`, `HAMMERJS` dan `Browser Animation` untuk Angular Material telah terpasang.

2. Checks

  ```bash
  npm show @angular/material version
  8.2.3
  ```

## Time Picker

Salah satu kekurangan Google Material yang sampai sekarang belum dipenuhi adalah pembuatan widget untuk Time Picker. Berikut adalah pemasangan time picker dari https://www.npmjs.com/package/amazing-time-picker-view24h.

Jika pada masa yang akan datang diketemukan element yang lebih baik, bisa disubstitusi.

0. Installation

  ```bash
  $ npm i amazing-time-picker-view24h --save
  ```

1. Hasil,

  ```bash
  npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.

  > core-js@2.6.11 postinstall /home/wandyatmono/projects/jago/frontend/node_modules/amazing-time-picker-view24h/node_modules/core-js
  > node -e "try{require('./postinstall')}catch(e){}"

  Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

  The project needs your help! Please consider supporting of core-js on Open Collective or Patreon: 
  > https://opencollective.com/core-js 
  > https://www.patreon.com/zloirock 

  Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)

  npm WARN @angular/http@7.2.15 requires a peer of @angular/core@7.2.15 but none is installed. You must install peer dependencies yourself.
  npm WARN @angular/http@7.2.15 requires a peer of @angular/platform-browser@7.2.15 but none is installed. You must install peer dependencies yourself.
  npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.11 (node_modules/fsevents):
  npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.11: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

  + amazing-time-picker-view24h@1.5.4
  added 7 packages from 9 contributors and audited 20998 packages in 40.191s

  23 packages are looking for funding
    run `npm fund` for details

  found 0 vulnerabilities
  ```

CATATAN: Setiap kali ada kebutuhan implementasi di subversion selanjutnya. Secara disiplin harus dilakukan,

- Eksperimen
- Pembuatan Guide

Dengan rapi dan jelas.