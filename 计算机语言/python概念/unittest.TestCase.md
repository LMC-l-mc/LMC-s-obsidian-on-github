一种测试格式：
```
import unittest

# 【规则 1：外壳格式】
# 必须定义一个类，并且这个类必须继承 unittest.TestCase
class TestMyFeature(unittest.TestCase):

    # 【规则 2：准备格式】（可选）
    # 方法名必须严格叫 setUp，用于准备测试环境
    def setUp(self):
        self.data = [1, 2, 3]

    # 【规则 3：测试方法格式】
    # 方法名必须以 test_ 开头，这是框架自动发现测试的唯一标识
    def test_first_feature(self):
        # 【规则 4：断言格式】
        # 必须使用 self.assertXXX() 系列方法来判断对错，而不是自己写 if/else
        self.assertEqual(len(self.data), 3)

    # 可以有多个测试方法，只要以 test_ 开头即可
    def test_second_feature(self):
        self.assertTrue(True)

    # 【清理格式】（可选）
    # 方法名必须严格叫 tearDown，用于清理测试环境
    def tearDown(self):
        self.data = None
```