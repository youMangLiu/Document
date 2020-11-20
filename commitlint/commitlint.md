# Create a package.json if needed
npm init

# For Windows:
npm install --save-dev @commitlint/config-conventional @commitlint/cli
# Install commitlint cli and conventional config
npm install --save-dev @commitlint/{cli,config-conventional}
# Configure commitlint to use conventional config
echo "module.exports = {extends: ['@commitlint/config-conventional']};" > commitlint.config.js

npm install --save-dev husky

# This allows us to add git hooks directly into our package.json via the husky.hooks field.
"husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  }
  
rule配置说明:：rule由name和配置数组组成，如：'name:[0, 'always', 72]'，数组中第一位为level，可选0,1,2，0为disable，1为warning，2为error，第二位为应用与否，可选always|never，第三位该rule的值。  