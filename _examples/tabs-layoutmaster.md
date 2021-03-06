---
layout: example
title: Tabs using LayoutMaster
synopsis: Interesting transitions between pages with LayoutMaster
date: 2015-06-17 00:00:00
tags:
- Layout
- Tabs
- Menu
uxConcepts:
- LayoutMaster
- LayoutAnimation
- ux:Global
- Grid
- ux:Class
- StatusBarBackground
- BottomBarBackground
preview-image: tabs-layoutmaster.png
preview-video: HaVCa7AK73o
---
This example shows how one can achieve a tabview with an animated indicator showing which tab is selected. The example achieves this by changing the `LayoutMaster` of an element along with a `LayoutAnimation` trigger, which allows one to animate elements between different layouts.

<!-- snippet-begin:code/MainView.ux:AppUX -->

```
<App Background="#eee">

    <Font ux:Global="RobotoMedium" File="Roboto-Medium.ttf" />

    <Panel ux:Class="Tab" ClipToBounds="false" Margin="0,0,0,4" Background="#bdc3c7">
        <string ux:Property="Text" />
        <Text Value="{ReadProperty Text}" Color="#FFF" Font="RobotoMedium" Alignment="Center" />
    </Panel>

    <Rectangle ux:Name="indicator" LayoutMaster="page1Tab" Alignment="Bottom" Height="4" Color="#6c7a89">
        <LayoutAnimation>
            <Move RelativeTo="WorldPositionChange" X="1" Duration="0.4" Easing="BackIn"/>
        </LayoutAnimation>
    </Rectangle>

    <Text ux:Class="WelcomeText" FontSize="30" Alignment="Center"/>

    <DockPanel>
        <StatusBarBackground Dock="Top" />
        <BottomBarBackground Dock="Bottom" />

        <Grid Dock="Top" ColumnCount="3" Height="50" Background="#bdc3c7">
            <Panel ux:Name="page1Tab">
                <Tab Text="Page 1">
                    <Clicked>
                        <Set navigation.Active="page1" />
                    </Clicked>
                </Tab>
            </Panel>
            <Panel ux:Name="page2Tab">
                <Tab Text="Page 2">
                    <Clicked>
                        <Set navigation.Active="page2" />
                    </Clicked>
                </Tab>
            </Panel>
            <Panel ux:Name="page3Tab">
                <Tab Text="Page 3">
                    <Clicked>
                        <Set navigation.Active="page3" />
                    </Clicked>
                </Tab>
            </Panel>
        </Grid>

        <PageControl ux:Name="navigation">
            <Page ux:Name="page1" Background="#eee">
                <WhileActive Threshold="0.5">
                    <Set indicator.LayoutMaster="page1Tab" />
                </WhileActive>
                <WelcomeText>Welcome to Page 1</WelcomeText>
            </Page>
            <Page ux:Name="page2" Background="#abb7b7">
                <WhileActive Threshold="0.5">
                    <Set indicator.LayoutMaster="page2Tab" />
                </WhileActive>
                <WelcomeText>Welcome to Page 2</WelcomeText>
            </Page>
            <Page ux:Name="page3" Background="#f2f1ef">
                <WhileActive Threshold="0.5">
                    <Set indicator.LayoutMaster="page3Tab" />
                </WhileActive>
                <WelcomeText>Welcome to Page 3</WelcomeText>
            </Page>
        </PageControl>

    </DockPanel>
</App>
```

<!-- snippet-end -->
