# cmp-im-flypy

用于[cmp-im](https://github.com/yehuohan/cmp-im)的中文码表:

- flypy: 小鹤音形

# 安装

## 使用Lazyvim安装

在`~/.config/nvim/lua/plugins`下新建一个`cmp-im.lua`文件，输入如下内容，之后重新打开nvim就会自动安装

```lua
return {
  -- 安装 cmp-im 插件
  {
    "yehuohan/cmp-im",
    dependencies = {
      "hrsh7th/nvim-cmp", -- 依赖 nvim-cmp 插件
      "hitdp/cmp-im-flypy", -- 依赖 cmp-im-flypy 插件
    },
    config = function()
      -- 在此处进行 cmp-im 的配置
      require("cmp_im").setup({
        -- 启用输入法
        enable = true,
        -- 设置输入法表
        tables = require("cmp_im_flypy").tables({ "flypy" }),
      })
      -- 设置快捷键切换中文输入
      vim.keymap.set({ "n", "v", "c", "i" }, "<M-;>", function()
        vim.notify(string.format("IM is %s", require("cmp_im").toggle() and "enabled" or "disabled"))
      end)

      -- 设置 nvim-cmp 的补全源
      require("cmp").setup({
        sources = {
          { name = "IM" }, -- 添加 IM 补全源
          -- 其他补全源...
        },
        -- 设置按键映射
        mapping = {
          -- 将 <Space> 键映射为选择输入法的补全项
          ["<Space>"] = require("cmp").mapping.confirm({ select = true }),
          -- 其他按键映射...
        },
      })
    end,
  },
}
```

Much thanks for tables from [ZFVimIM#db-samples](https://github.com/ZSaberLv0/ZFVimIM#db-samples).
