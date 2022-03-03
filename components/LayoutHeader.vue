<template>
    <header>
      <div>
        <b-navbar toggleable="lg" type="dark" class="bg-dark">
            <b-navbar-brand href="/">小人旅人</b-navbar-brand>
            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
            <b-collapse id="nav-collapse" is-nav>
                <b-navbar-nav>
                    <b-nav-item href="/concept">コンセプト</b-nav-item>
                    <b-nav-item href="/trip">旅行先</b-nav-item>
                    <b-nav-item href="/information">お知らせ</b-nav-item>
                </b-navbar-nav>
                <b-navbar-nav class="ml-auto">
                    <a href="https://twitter.com/share?ref_src=twsrc%5Etfw" class="twitter-share-button" data-show-count="false">Tweet</a>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
                </b-navbar-nav>
            </b-collapse>
        </b-navbar>
    </div>
  </header>
</template>

<script>
export default {
    name: 'LayoutHeader',
    date() {
        return {
            isOpen: false,
        }
    }
}
</script>