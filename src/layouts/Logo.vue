<script lang="tsx">
  import { defineComponent, PropOptions } from 'compatible-vue';

  // hooks
  import { useDesign } from '@/hooks/core/useDesign';
  import { useSetting } from '@/hooks/core/useSetting';

  import { pageEnum } from '@/enums/pageEnum';
  import logo from '@/assets/images/logo.png';

  export default defineComponent({
    name: 'Logo',
    props: {
      showTitle: {
        type: Boolean,
        default: true,
      } as PropOptions<boolean>,
    },
    setup(props, { root }) {
      const { prefixCls } = useDesign('logo');
      const { globSetting } = useSetting();

      function handleGoHome() {
        root.$router.push(pageEnum.BASE_HOME);
      }
      return () => {
        const { showTitle } = props;

        return (
          <section class={`${prefixCls}-wrap`} onClick={handleGoHome}>
            <img src={logo} class={`${prefixCls}__img`} />
            {showTitle && <section class={`${prefixCls}__title`}>{globSetting.title}</section>}
          </section>
        );
      };
    },
  });
</script>
<style lang="less" scoped>
  @import (reference) '~@design';
  @prefix-cls: ~'@{namespace}-logo';

  .@{prefix-cls} {
    &-wrap {
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }

    &__img {
      .size(40px);
    }

    &__title {
      width: 130px;
      margin-left: 8px;
      font: italic 2em Georgia, serif;
      font-size: 24px;
      // word-break: break-all;
      .respond-to(xsmall-only, { display: none;});
      .respond-to(small-only, { display: none;});
    }
  }
</style>
