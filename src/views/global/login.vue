<!-- 
 * @description: 
 * @fileName: index.vue 
 * @author: zcf 
 * @date: 2022-01-11 15:05:47 
!-->
<template>
  <div class="login-bg">
    <video
      src="@/assets/video/bg.mp4"
      loop="loop"
      autoplay="autoplay"
      muted="muted"
    ></video>
    <div class="login-wrapper">
      <div class="title">
        <span>RBAC后台管理系统</span>
      </div>
      <el-card
        class="login-card width-400"
        v-loading="loading"
        element-loading-background="rgba(0, 0, 0, 0.1)"
      >
        <el-form
          :model="form"
          :rules="rules"
          ref="refForm"
          @keyup.enter="submit()"
          status-icon
        >
          <el-form-item prop="username">
            <el-input v-model="form.username" placeholder="账户" clearable>
              <template #prefix>
                <span><g-svg name="user" /></span>
              </template>
            </el-input>
          </el-form-item>
          <el-form-item prop="password">
            <el-input
              v-model="form.password"
              placeholder="密码"
              show-password
              clearable
            >
              <template #prefix>
                <span><g-svg name="lock" /></span>
              </template>
            </el-input>
          </el-form-item>
          <el-form-item prop="code">
            <el-row :gutter="20">
              <el-col :span="16" class="height-36">
                <el-input v-model="form.code" placeholder="验证码" clearable>
                  <template #prefix>
                    <span><g-svg name="verification" /></span>
                  </template>
                </el-input>
              </el-col>
              <el-col :span="8" class="height-36 cursor-pointer">
                <img
                  :src="captchaPath"
                  @click="captcha()"
                  alt="验证码"
                  class="width-full"
                />
              </el-col>
            </el-row>
          </el-form-item>
          <el-form-item>
            <el-button
              class="margin_t-22 width-full"
              type="primary"
              @click="submit()"
              >登录</el-button
            >
          </el-form-item>
        </el-form>
      </el-card>
    </div>
  </div>
</template>

<script>
import {
  defineComponent,
  reactive,
  toRefs,
  ref,
  onBeforeMount,
  nextTick,
} from "vue";
import { useRouter } from "vue-router";
import { useStore } from "vuex";

import { getUUID } from "@/utils/index";

import { captchaApi } from "@/api/login";

export default defineComponent({
  setup() {
    const router = useRouter();
    const store = useStore();

    const data = reactive({
      loading: false,
      captchaPath: "",
    });

    const refForm = ref();
    const form = reactive({
      username: "test",
      password: "test",
      uuid: "",
      code: "",
    });
    const rules = reactive(
      (function () {
        return {
          username: [
            { required: true, message: "账户不能为空", trigger: "blur" },
          ],
          password: [
            { required: true, message: "密码不能为空", trigger: "blur" },
          ],
          code: [
            { required: true, message: "验证码不能为空", trigger: "blur" },
          ],
        };
      })()
    );

    /**
     * @description: 获取验证码图片
     * @param {*}
     * @return {*}
     * @author: gumingchen
     */
    const captcha = () => {
      form.uuid = getUUID();
      data.captchaPath = captchaApi({ uuid: form.uuid });
    };

    /**
     * @description: 登录表单提交
     * @param {*}
     * @return {*}
     * @author: gumingchen
     */
    const submit = () => {
      refForm.value.validate((valid) => {
        if (valid) {
          data.loading = true;
          store.dispatch("user/login", form).then((r) => {
            if (r) {
              router.push({ name: "home" });
            } else {
              captcha();
            }
            nextTick(() => {
              data.loading = false;
            });
          });
        }
      });
    };

    onBeforeMount(() => {
      captcha();
    });

    return {
      ...toRefs(data),
      refForm,
      form,
      rules,
      captcha,
      submit,
    };
  },
});
</script>

<style lang="scss" scoped>
.login-bg {
  width: 100%;
  height: 100%;
  // background-color: #333;
  video {
    position: fixed; //视频定位方式设为固定
    right: 0;
    bottom: 0; //视频位置
    min-width: 100%;
    min-height: 100%; //不会因视频尺寸造成页面需要滚动
    width: auto;
    height: auto; //尺寸保持原视频大小
    z-index: -100; //z轴定位，小于0即可
    -webkit-filter: blur(4px); //添加灰度蒙版，如果设定为100%则视频显示为黑白
  }
  .login-wrapper {
    width: 500px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    .title {
      position: absolute;
      top: -28%;
      background-color: transparent;
      font-size: 40px;
      font-weight: 600;
      letter-spacing: 6px;
      color: #fff;
    }
  }
  .login-card {
    background-color: rgba(255, 255, 255, 0.5);
  }
}
</style>
